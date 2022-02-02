---
layout: post
title: In-memory caching in Xamarin apps
date: 2017-09-26 06:53:38.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- ".NET"
- C#
- caching
- mobile
- Xamarin
meta:
  _edit_last: '1'
  layout: default
  feature_size: blank
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  builder_switch_frontend: '0'
  dsq_thread_id: '6171933509'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/in-memory-caching-in-xamarin-apps/"
---
<p><img class="aligncenter size-full wp-image-19203" src="{{ site.baseurl }}/assets/2017/09/cpu.png" alt="CPU" width="1440" height="614" /></p>
<p>Recently we added in-memory caching to <a href="https://aka.ms/azureapp">Azure App</a>. You can try it out now on <a href="https://aka.ms/azureapp/ios">iOS</a> and <a href="https://aka.ms/azureapp/android">Android</a>!</p>
<p>It turns out <a href="http://www.go-mono.com/status/status.aspx?reference=4.5&amp;profile=4.5&amp;assembly=System.Runtime.Caching">Mono doesn't have <code>System.Runtime.Caching</code> namespace</a>, which makes it easy to implement caching for .NET apps. We had to find another way.</p>
<h3>Caching libraries for Xamarin</h3>
<p>We looked at a few libraries for caching (e.g., <a href="https://www.nuget.org/packages/MemoryCache/">MemoryCache</a> and <a href="https://github.com/akavache/Akavache/">Akavache</a>), but surprisingly none of them manage cache size and memory. They simply add items to Dictionary, and if you add too many you get <code>OutOfMemoryException</code>.</p>
<p>It may not be an issue for many applications, but in <a href="https://aka.ms/azureapp">Azure App</a> we need to take into account users who has multiple subscriptions with thousands of resources.</p>
<p>BTW: Akavache is a great library. Besides in-memory cache it also supports persistent cache, have clean APIs and a lot of great documentation.</p>
<h3>Implementing in-memory cache</h3>
<p>After browsing internets and asking people at <a href="https://xamarinchat.slack.com">Xamarin chat</a> we didn't find anything that would work for us, and we decided to implement in-memory cache by ourselves.</p>
{% highlight csharp %}
public class InMemoryCache<t> : IInMemoryCache<t>
{
    private const int LimitedCacheThreshold = 1000;

    private class Reference
    {
        private int _hitCount = 0;

        public DateTimeOffset Timestamp
        {
            get;
            private set;
        }

        public T Data
        {
            get;
            private set;
        }

        public void AddRef()
        {
            Interlocked.Increment(ref _hitCount);
        }

        public int ResetRef()
        {
            var count = _hitCount;
            _hitCount = 0;
            return count;
        }

        public static Reference Create(T obj)
        {
            return new Reference()
            {
                Timestamp = DateTimeOffset.Now,
                Data = obj,
            };
        }

        private Reference()
        {
        }
    }

    private readonly ConcurrentDictionary<string, WeakReference<reference>> _weakCache;
    private readonly ConcurrentDictionary<string, Reference> _limitedCache;
    private readonly ConcurrentDictionary<string, Task<t>> _pendingTasks;

    private InMemoryCache()
    {
        _weakCache = new ConcurrentDictionary<string, WeakReference<reference>>(StringComparer.Ordinal);
        _limitedCache = new ConcurrentDictionary<string, Reference>(StringComparer.Ordinal);
        _pendingTasks = new ConcurrentDictionary<string, Task<t>>(StringComparer.Ordinal);
    }

    public static IInMemoryCache<t> Create()
    {
        return new InMemoryCache<t>();
    }

    public async Task<t> GetOrAdd(string key, DateTimeOffset expiration, Func<string, Task<t>> addFactory)
    {
        WeakReference<reference> cachedReference;

        if (_weakCache.TryGetValue(key, out cachedReference))
        {
            Reference cachedValue;
            if (cachedReference.TryGetTarget(out cachedValue) || cachedValue != null)
            {
                if (cachedValue.Timestamp > expiration)
                {
                    cachedValue.AddRef();
                    return cachedValue.Data;
                }
            }
        }

        try
        {
            var actualValue = await _pendingTasks.GetOrAdd(key, addFactory);

            if (_limitedCache.Count > LimitedCacheThreshold)
            {
                var keysToRemove = _limitedCache
                    .Select(item => Tuple.Create(
                        item.Value.ResetRef(),
                        item.Value.Timestamp,
                        item.Key))
                    .ToArray()
                    .OrderBy(item => item.Item1)
                    .ThenBy(item => item.Item2)
                    .Select(item => item.Item3)
                    .Take(LimitedCacheThreshold / 2)
                    .ToArray();

                foreach (var k in keysToRemove)
                {
                    Reference unused;
                    _limitedCache.TryRemove(k, out unused);
                }
            }

            var reference = Reference.Create(actualValue);
            _weakCache[key] = new WeakReference<reference>(reference);
            _limitedCache[key] = reference;

            return actualValue;
        }
        finally
        {
            Task<t> unused;
            _pendingTasks.TryRemove(key, out unused);
        }
    }
}
{% endhighlight %}
<p>We use two layers of caching. First is using <code>WeakReference</code> that leaves memory management to Garbage Collector. As GC is not very predictable and sometimes may unnecessary release some reference, we have second layer of caching. We call it <code>_limitedCache</code>, and it keeps objects in memory until capacity reach 1000 objects. Then we remove half (500), least used objects from dictionary. Because the same objects are being kept in two dictionaries, the <code>WeakReference</code> will never be released as long as object is in <code>_limitedCache</code>. Thus, we always check only if object is present in <code>_weakCache</code>.</p>
<p>There is also third dictionary that keeps track of pending tasks that are responsible for getting data. This prevents us from sending the same requests more than once if object is not in cache yet.</p>
<h3>Summary</h3>
<p>What is great about building apps with Xamarin is the ability to share code across platforms. When we were implementing cache, we didn't touch any platform specific code. All work was done in <a href="https://developer.xamarin.com/guides/cross-platform/application_fundamentals/pcl/introduction_to_portable_class_libraries/">Portable Class Library</a>.</p>
<p>Adding cache to <a href="https://aka.ms/azureapp">Azure App</a> helped not only to decrease user's network data usage, but also to improve performance significantly!</p>
<p>If you need in-memory cache for your app, go ahead and use the above code snippet! If you are looking for persistent cache then consider using <a href="https://github.com/akavache/Akavache/">Akavache</a>.</p>
<p>Are you caching? How? Why? Why not?</p>

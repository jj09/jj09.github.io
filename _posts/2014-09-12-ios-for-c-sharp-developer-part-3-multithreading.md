---
layout: post
title: 'iOS for C# Developer - part 3: multithreading'
date: 2014-09-12 00:07:07.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- ios
- iOS for C# Developer
- Objective-C
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
  _syntaxhighlighter_encoded: '1'
  builder_switch_frontend: '0'
  dsq_thread_id: '3010447346'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/ios-for-c-sharp-developer-part-3-multithreading/"
---
<p>This post is part of the series: <a title="iOS for C# Developer" href="http://jj09.net/tag/ios-for-c-developer/"><strong>iOS for C# Developer</strong></a>. Previous parts:</p>
<ul>
<li><a title="iOS for C# Developer – part 1: Classes and creating objects" href="http://jj09.net/ios-c-sharp-developer-part-1-classes-and-creating-objects/">part 1 (Classes and creating objects)</a></li>
<li><a title="iOS for C# Developer – part 2: strings" href="http://jj09.net/ios-for-c-sharp-developer-part2-strings/">part 2 (strings)</a></li>
</ul>
<p>The most typical scenario to use multithreading is to maintain responsive UI when we do some resource-consuming computation.</p>
<h3>C#</h3>
<p>Let's consider simple button click action in C#:</p>

{% highlight csharp %}
private void Button_Click(object sender, RoutedEventArgs e)
{
    this.status.Content = "Computing...";
    Compute();
    this.status.Content = "Done";
}

private void Compute()
{
    Thread.Sleep(5000);            
}

{% endhighlight %}

<p>Method <code>Compute()</code> is a CPU-intensive operation (simulated by <code>Sleep()</code> function).</p>
<p>Above code will block UI during computation. To keep UI responsive, computation has to take place in a separate thread. It can be done easily using <code>async</code>/<code>await</code> keywords:</p>

{% highlight csharp %}
private async void Button_Click(object sender, RoutedEventArgs e)
{
    this.status.Content = "Computing...";
    await Compute();
    this.status.Content = "Done";
}

private async Task Compute()
{
    await Task.Factory.StartNew(() =&gt;
    {
        Thread.Sleep(5000);
    });
}

{% endhighlight %}

<h3>iOS</h3>
<p>This is equivalent (single-threaded) button click handler in iOS:</p>

{% highlight csharp %}
- (IBAction)buttonClick:(id)sender
{
    self.status.text = @"Computing...";
    [self compute];
    self.status.text = @"Done";
}

- (void)compute
{
    [NSThread sleepForTimeInterval:5];
}

{% endhighlight %}

<p>Multithreaded version is a little bit different. In Objective-C, there is no syntax similar to <code>async</code>/<code>await</code>. Thus, status update has to be invoked by background thread explicitly. Additionally, every UI operation (in this case: label text update) has to be done in the main thread. Below code, use <a href="https://developer.apple.com/library/ios/documentation/General/Conceptual/ConcurrencyProgrammingGuide/OperationQueues/OperationQueues.html">Dispatch Queues</a>, which is the easiest and recommended way for multithreading scenarios:</p>

{% highlight csharp %}
- (IBAction)buttonClick:(id)sender
{
    self.status.text = @"Computing...";
    [self compute];
}

- (void)compute
{
    dispatch_queue_t queue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
    dispatch_async(queue, ^{
        [NSThread sleepForTimeInterval:5];
        dispatch_async(dispatch_get_main_queue(), ^{
            self.status.text = @"Done";
        });
    });
}

{% endhighlight %}

<p>This multithreaded code will look pretty similar in Swift.</p>
<h3>Summary</h3>
<p>Invoking background threads is much easier from developer perspective in C#. Code is concise and more readable. Multithreading in Objective-C introduce some overhead, but it is not very hard to handle.</p>

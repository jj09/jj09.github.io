---
layout: post
title: 'iOS for C# Developer - part 2: strings'
date: 2014-09-05 11:28:00.000000000 -07:00
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
  builder_switch_frontend: '0'
  dsq_thread_id: '2991213985'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/ios-for-c-sharp-developer-part2-strings/"
---
<p>This post is part of the series: <a title="iOS for C# Developer" href="http://jj09.net/tag/ios-for-c-developer/"><strong>iOS for C# Developer</strong></a>. First part can be found <a title="iOS for C# Developer – part 1: Classes and creating objects" href="http://jj09.net/ios-c-sharp-developer-part-1-classes-and-creating-objects/">here</a>.</p>
<p>String operations in Objective-C are very verbose in comparison to C#.</p>
<p>Let's assume the following string definition for all below examples:</p>

{% highlight objc %}
NSString *str = @"Some string. Another string.";
{% endhighlight %}

<h3>Concatenation</h3>
<p>I think this is the most common operation. In C# it is very simple:</p>

{% highlight csharp %}
string result += " Appended string.";
{% endhighlight %}

<p>* For concatenation in C#, consider using <code>StringBuilder</code> class (if performance matters).</p>
<p>In Objective-C, <code>NSMutableString</code> type has to be used. Thus, if we have <code>NSString</code> created, we have to do the following:</p>

{% highlight objc %}
NSMutableString *temp = [[NSMutableString alloc] initWithString:str];
[temp stringByAppendingString:@" Appended string."];
str = temp;
{% endhighlight %}

<p>A bit of work, huh?</p>
<h3>Substring</h3>
<p>To get substring from letter 3 to 7 in C#:</p>

{% highlight csharp %}
string result = str.Substring(3,5);
{% endhighlight %}

<p>In Objective-C:</p>

{% highlight objc %}
NSString *result = [str substringWithRange:NSMakeRange(3,5)];
{% endhighlight %}

<p>Pretty straightforward.</p>
<h3>Split</h3>
<p>To split sentences in our sample string in C#, we would do:</p>

{% highlight csharp %}
string[] result = str.Split(". ");
{% endhighlight %}

<p>In Objective-C:</p>

{% highlight objc %}
NSArray *result = [str componentsSeparatedByString:@". "];
{% endhighlight %}

<p>Also, pretty similar.</p>
<h3>Replace</h3>
<p>This operation is much more verbose than its equivalent in C#. To replace spaces with underscores, in C# we do:</p>

{% highlight csharp %}
string result = str.Replace(" ", "_");
{% endhighlight %}

<p>In Objective-C:</p>

{% highlight objc %}
NSString *result = [str stringByReplacingOccurrencesOfString:@" " withString:@"_"];
{% endhighlight %}

<p>Looks pretty the same, but long, custom names preceding actual parameters make code unnecessary long (IMO).</p>
<h3>Real-world example</h3>
<p>Usually we need a few string operations working together. Let's apply above operations together. For example: we want to get only the second sentence from our string with underscores instead of spaces.</p>
<p>In C#:</p>

{% highlight csharp %}
string result = str.Split(new [] {". "}, StringSplitOptions.RemoveEmptyEntries)[1].Replace(' ','_');
{% endhighlight %}

<p>In Objective-C:</p>

{% highlight objc %}
NSString *result = [[str componentsSeparatedByString:@". "][1] stringByReplacingOccurrencesOfString:@" " withString:@"_"];
{% endhighlight %}

<h3>Summary</h3>
<p>Some of above operations are easier in Swift (e.g., <a href="http://stackoverflow.com/questions/24034174/how-do-i-concatenate-strings-in-swift">concatenation</a> looks the same like in C#), but some are still very verbose (e.g., <a href="http://stackoverflow.com/questions/24044851/how-do-you-use-string-substringwithrange-or-how-do-ranges-work-in-swift">substring</a>, <a href="http://stackoverflow.com/questions/24200888/any-way-to-replace-characters-on-swift-string">replace</a>). However, the syntax is more similar to C#. The message passing syntax is something you need to get use to in Objective-C, not only in case of string operations.</p>

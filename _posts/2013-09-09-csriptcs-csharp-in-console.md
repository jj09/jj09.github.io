---
layout: post
title: scriptcs - C# in console
date: 2013-09-09 10:30:23.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
- tools
tags:
- ".NET"
- C#
- console
- Open Source
- scriptcs
- windows
meta:
  _yoast_wpseo_linkdex: '59'
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _yoast_wpseo_focuskw: scriptcs tutorial
  _syntaxhighlighter_encoded: '1'
  dsq_thread_id: '1740792519'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/csriptcs-csharp-in-console/"
---
<p>It was always bothering me, when I wanted to run one simple command, and I needed to create new C# console project in Visual Studio to do that. With scriptcs I can finally do that in console. Project <a href="http://scriptcs.net/">scriptcs</a> allows you to run single commands and also C# script files.</p>

<h3>Installation</h3>
<p>The easiest way to install scriptcs is <a href="http://chocolatey.org/">Chocolatey</a> ('apt-get' for windows). If you didn't hear about it, you should definitely try it out. To install Chocolatey run the following command in console:</p>
<p><code>@powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%systemdrive%\chocolatey\bin</code></p>
<p>Once you have Chocolatey installed, you can install scriptcs:</p>
<p><code>cinst scriptcs</code></p>
<p>Chocolatey will install scriptcs to <em>%APPDATA%\scriptcs\</em>. You need to update your PATH accordingly, to easily run it from command line.</p>

<h3>Getting started</h3>
<p>Once scriptcs is installed and added to your PATH, you can run it with <em>scriptcs</em> command:</p>
{% highlight console %}
C:\> scriptcs
scriptcs (ctrl-c or blank to exit)
> var message = "Hello, world!";
> Console.WriteLine(message);
Hello, world!
>
C:\>
{% endhighlight %}

<p>You can also create a script hello.csx:</p>
{% highlight csharp %}
var message = "Hello, world!";
Console.WriteLine(message);
{% endhighlight %}

<p>And run it from command line:</p>
{% highlight console %}
C:\>scriptcs hello.csx
Hello, world!
{% endhighlight %}

<p>You can find more about scriptcs on <a href="http://scriptcs.net/">scriptcs.net</a>.</p>

<p><b>EDIT:</b> You don't even need <code>Console.WriteLine</code> to print variables (thanks <a href="http://www.strathweb.com/">Filip W.</a>):</p>

{% highlight console %}
C:\>scriptcs
scriptcs (ctrl-c or blank to exit)
> var message = "Hello, scriptcs!";
> message
Hello, scriptcs!
> int four = 2 + 2;
> four
4
>
{% endhighlight %}

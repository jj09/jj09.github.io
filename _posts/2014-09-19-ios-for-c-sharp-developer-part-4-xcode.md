---
layout: post
title: 'iOS for C# Developer - part 4: Xcode'
date: 2014-09-19 09:18:57.000000000 -07:00
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
  _oembed_56f079cb0ecd80023c72bbffaa52f9b9: "{{unknown}}"
  _oembed_dd74c50ab39cf5e4b3d62cd65519af00: "{{unknown}}"
  builder_switch_frontend: '0'
  dsq_thread_id: '3033796231'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/ios-for-c-sharp-developer-part-4-xcode/"
---
<p>This post is part of the series: <a title="iOS for C# Developer" href="http://jj09.net/tag/ios-for-c-developer/"><strong>iOS for C# Developer</strong></a>. Previous parts:</p>
<ul>
<li><a title="iOS for C# Developer – part 1: Classes and creating objects" href="http://jj09.net/ios-c-sharp-developer-part-1-classes-and-creating-objects/">part 1 (Classes and creating objects)</a></li>
<li><a title="iOS for C# Developer – part 2: strings" href="http://jj09.net/ios-for-c-sharp-developer-part2-strings/">part 2 (strings)</a></li>
<li><a title="iOS for C# Developer – part 3: multithreading" href="http://jj09.net/ios-for-c-sharp-developer-part-3-multithreading/">part 3 (multithreading)</a></li>
</ul>
<p>C# developers works with Visual Studio. Recently, some are trying to switch to SublimeText. However, I will assume that you, as C# Developer are familiar with VS. To write iOS applications, you need Xcode. I haven't heard about nobody who created an working app in a different editor (more advanced than Hello World).</p>
<p>In this post I would like to provide a few tips that will help you to get started and be productive.</p>
<p>The first thing that is worth to mention is the fact that Xcode is free. You cannot test you apps on the iPhone or iPad before you pay $99 though. You need to be satisfied with simulator.</p>
<h3>Key shortcuts</h3>
<p>For the beginning, remember three:</p>
<ul>
<li>⇧ + ⌘ + O - quick open (equivalent to CTRL+, in VS2013 or CTRL+T in ReSharper)</li>
<li>⌥ + click - jump to documentation (when clicked on class/interface)</li>
<li>⌘ + L - jump to specified line of code</li>
</ul>
<p>This three will definitely help you to get productive at the beginning. You can find more in <a href="https://cloud.github.com/downloads/Machx/Xcode-Keyboard-Shortcuts/Xcode_Shortcuts.pdf">this cheat-sheet</a>.</p>
<h3>Debugging</h3>
<p>In order to debug application in VS, you have to run it in debug mode. In Xcode, when you run the app on emulator it is always in debug mode. Thus, you just need to set the break-point (by mouse click on the line number, like in VS, or by ⌘ + \ shortcut) and run the app (⌘ + R). Once break-point is reached you can step over (F6), step into (F7) or step out (F8).</p>
<p>Very useful during debugging is dumping objects into console with <code>NSLog</code> function:</p>
<pre class="lang:objc decode:true">NSLog(jsonString);</pre>
<p>This outputs, e.g., JSON string to the console, which allows you to inspect it.</p>
<p>To get more flavor of debugging, check <a href="https://developer.apple.com/library/ios/documentation/ToolsLanguages/Conceptual/Xcode_Overview/DebugYourApp/DebugYourApp.html">Apple documentation</a> and <a href="http://www.raywenderlich.com/28289/debugging-ios-apps-in-xcode-4-5">Brian Moakley's blog post</a>.</p>
<h3>Playgrounds</h3>
<p>The latest version of Xcode (v6), which introduce support for Swift language, adds also very handy feature: Playgrounds. It allows you write and test simple Swift programs, without using iOS emulator. Playgrounds are useful especially, when you are testing some complex logic. They are very powerful. You can use them even to test drawing (still without running iOS emulator). To see it in action, check <a href="https://www.youtube.com/watch?v=xtZl1_zc3gg">this demo</a>.</p>
<h3>Summary</h3>
<p>Xcode is very nice IDE. Works very smooth, and breaks very rarely. I wish there was more code snippets (like it is in Visual Studio, especially with ReSharper or WebEssentials). Xcode could also adapt rich debugging experience from VS (e.g., inspecting object variable after moving mouse pointer in top of them). I find it hard to work with this IDE on small screen (like MacBook display). To get comfortable, I need at least 22-24". But that is just my opinion. What do you think?</p>

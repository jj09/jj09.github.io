---
layout: post
title: Getting started with Xamarin in 2016
date: 2016-05-30 23:50:33.000000000 -07:00
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
  _wp_old_slug: getting-started-with-xamarin
  _oembed_20d76ceebd81d23002cb716f4a1fa358: "{{unknown}}"
  enclosure: "https://s3.amazonaws.com/dnr/dotnetrocks_1303_xamarinforms.mp3\r\n51647050\r\naudio/mpeg\r\n"
  dsq_thread_id: '4871211990'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/getting-started-with-xamarin-in-2016/"
---
<p><img class="aligncenter size-full wp-image-14711" src="{{ site.baseurl }}/assets/2016/05/Xamarin_Blue_Logo.png" alt="Xamarin" width="600" height="145" /></p>
<p>Xamarin is a cross-platform mobile development framework that allows you to build native mobile applications with C# and share code between them. There are two approaches:</p>
<ul>
<li>native Xamarin - write native UI code in C# (views cannot be shared, business logic can be shared)</li>
<li>Xamarin.Forms - write shared UI in XAML (native controls are being generated, and business logic can be shared as well)</li>
</ul>
<p><img class="aligncenter size-full wp-image-14671" src="{{ site.baseurl }}/assets/2016/05/xamarin-vs-xamarinforms.jpg" alt="Xamarin vs Xamarin.Forms" width="638" height="359" /></p>
<p>The beauty of the first approach is ability to take advantage of Swift (iOS) or Java (Android) code samples, documentation, and community support. Swift/Java code can be easily translated into C#. In Xamarin.iOS app you have storyboards, ViewControllers and everything else you know from native iOS development. Similarly in Xamarin.Android - there are activities, fragments, action bars etc.</p>
<p>Xamarin.Forms on the other hand allows you to build apps faster. It's very good fit for business applications.</p>
<p>Which approach should you choose? <a href="http://stackoverflow.com/questions/32204807/when-to-use-xamarin-forms-vs-xamarin-native">Ask StackOverflow</a>.</p>
<h3>Resources to get started</h3>
<p>The great way to get started with Xamarin is <a href="https://www.xamarin.com/university">Xamarin University</a>. You can also find variety of <a href="https://app.pluralsight.com/library/search?i=1&amp;q1=course&amp;x1=categories&amp;q=xamarin">Xamarin courses at Pluralsight</a>. I especially recommend <a href="https://app.pluralsight.com/library/courses/ios-xamarin-from-start-to-store">Building Your First Xamarin.iOS App from Start to Store</a>, <a href="https://app.pluralsight.com/library/courses/android-xamarin-from-start-to-store">Building Your First Xamarin.Android App from Start to Store</a>, and <a href="https://app.pluralsight.com/library/courses/xamarin-forms-introduction">Introduction to Xamarin.Forms</a>.</p>
<p>Friend of mine, <a href="https://twitter.com/jamesmontemagno">James Montemagno</a> (Developer Evangelist at Xamarin), runs video series <a href="https://www.youtube.com/playlist?list=PLwOF5UVsZWUi1RARu_18It6gX7NKWwx85">Motz Codes Live</a> where he explores different areas of Xamarin: from internals of MVVM, through Xamarin Inspector, to using Azure as backend for Xamarin mobile apps. You can also find a bunch of his videos from variety of conferences on <a href="https://www.youtube.com/results?search_query=james+montemagno">youtube</a>.</p>
<p>Additionally, there is a bunch of <a href="https://developer.xamarin.com/guides/">guides</a>, <a href="https://developer.xamarin.com/recipes/">recipes</a>, and <a href="https://developer.xamarin.com/samples-all/">samples</a> at Xamarin website. The <a href="https://developer.xamarin.com/api/">official documentation</a> is also a good source of knowledge.</p>
<p>Many of you were asking about Xamarin.Forms on <a href="https://www.reddit.com/r/programming/comments/4ltyb7/getting_started_with_xamarin_in_2016/">reddit</a>. A lot has been changed in this area as well. Check out the latest, greatest Xamarin.Forms update from James on .NET Rocks:</p>
<p><audio preload="metadata" controls="controls"><source type="audio/mpeg" src="https://s3.amazonaws.com/dnr/dotnetrocks_1303_xamarinforms.mp3" /></audio></p>
<h3>Code sharing strategies</h3>
<p>One of the main advantages of Xamarin is code sharing. There are two ways to share code across platforms:</p>
<ul>
<li>Portable Class Library (PCL) - produces separated .dll</li>
<li>Shared Project - compiled into one assembly with platform specific projects (you can think about files in shared projects as they all are present in all platform specific projects)</li>
</ul>
<p>Most important differences:</p>
<ul>
<li>PCL can have referenced libraries, while shared project cannot.</li>
<li>When we want to test shared code then in PCL case it is enough to reference PCL project only in the test project, while shared project requires additionally to add reference for all references that are being used by Shared Project.</li>
<li>You cannot have platform specific code in PCL, while shared project allows that using <a href="https://developer.xamarin.com/guides/cross-platform/application_fundamentals/building_cross_platform_applications/part_4_-_platform_divergence_abstraction_divergent_implementation/#Conditional_Compilation">compiler directives</a>.</li>
</ul>
<p>You can learn more about code sharing <a href="https://docs.xamarin.com/guides/cross-platform/application_fundamentals/building_cross_platform_applications/sharing_code_options/">here</a>.</p>
<h3>Two apps - two approaches</h3>
<p>A few months ago I created two mobile apps with Xamarin, for 3 platforms (iOS, Android, UWP) and published them to 3 stores (App Store, Google Play, Windows Store):</p>
<ul>
<li><a href="https://github.com/jj09/ShoppingPad">Shopping Pad</a> - smart shopping list that allows you not only to create a shopping list, but also remembers items that you have purchased in the past, how often they have been purchased, and based on that suggests items for your next grocery store trip.</li>
<li><a href="https://github.com/jj09/BreadCrumbs">Bread Crumbs</a> - enables you to save your current location, and you can navigate to it later on (useful if you are in the new city, and you want to comeback to some place that you are "currently at")</li>
</ul>
<p>In Shopping Pad I used Portable Class Library to share code between platforms. In Bread Crumbs - Shared Project. I used SQLite for persistence in both apps, and the only difference I experienced was in creating SQLite connections. In PCL you need to create connection on "platform project" (you cannot do it from PCL). Shared Project allows you to use conditional compilation, and instantiate connection(s) in one file (using <a href="https://developer.xamarin.com/guides/cross-platform/application_fundamentals/building_cross_platform_applications/part_4_-_platform_divergence_abstraction_divergent_implementation/#Conditional_Compilation">compiler directives</a>).</p>
<p>I created unit tests (with xUnit) for Shopping Pad, and I was able to test entire app logic (for 3 platforms!) with only one test project. No platform specific code. Awesome!</p>
<p>Many times when I was looking for a solution to particular problem, I was able to reuse native iOS (Objective-C/Swift) or Android (Java) code samples, and translate them into C#.</p>
<p>Even for these two, small apps, shared code reuse was significant during development process. Especially in keeping consistency across platforms.</p>
<p>Both apps are available on App Store, Google Play, and Windows Store (<a href="http://jj09.github.io/ShoppingPad/">Shopping Pad</a>, <a href="http://jj09.github.io/BreadCrumbs/">Bread Crumbs</a>).</p>
<h3>Tips &amp; Tricks</h3>
<p>The struggle you may (and you probably will) experience at the beginning is platform setup. I recommend you to use Visual Studio simulators for Android (with Hyper-V) - they are faster. You need to have XCode installed on your Mac in order to run iOS apps built with Xamarin.</p>
<p>I develop Xamarin apps with Visual Studio on my ThinkPad X1, and use Mac only as host for running iOS apps. Some people run Windows on Mac with <a href="http://www.parallels.com/">Parallels</a>. Others use Xamarin Studio for iOS and Android, and switch to Windows only for UWP development. This will minimize the number of configuration issues, but will also give you worse development experience. I find Visual Studio much nicer for C#, and also for Xamarin development.</p>
<p><a href="https://docs.google.com/document/d/1wkG36pVcqo3enL5RSSv-haa-2_jSazsruatzPGbPqAM">Xamarin - Windows Setup guide</a> and <a href="https://docs.google.com/document/d/1moCCFj_QkNA7RSO-hvvPZr9R6eVW-ENSCkEmwZ8wGxc/">Xamarin - Mac OS X Setup guide</a> can help you get through configuration process. There is also fresh post from James about <a href="http://motzcod.es/post/145219135782/surface-book-setup-for-xamarin-developers">Setting Up Xamarin on Surface Book</a>.</p>
<p>During mobile apps development with Xamarin you will encounter some problems that will not occur when developing pure native apps with Swift and Java. To save you some time, here are the list of a few of typical problems, together with solutions:</p>
<ul>
<li><strong>Problem</strong>: connecting with iOS host sometimes will not work. <strong>Solution</strong>: update your Mac (and XCode), update Xamarin plugin for Visual Studio, make sure your XCode path in Visual Studio settings is correct, and restart both machines. If it does not help check other solutions <a href="https://forums.xamarin.com/discussion/55970/mac-agent-not-working-cant-connect">here</a>.</li>
<li><strong>Problem</strong>: iOS simulators not visible in Visual Studio. <strong>Solution</strong>: <a href="http://stackoverflow.com/questions/32913177/xamarin-for-visual-studio-not-showing-simulator-list">link</a>.</li>
<li><strong>Problem</strong>: Error: "Failed to add reference to 'System.Collections'. Please make sure that it is in the Global Assembly Cache.". <strong>Solution</strong>: add, manually, Droid/iOS dlls to references.</li>
<li><strong>Problem</strong>: free provisioning Xamarin.iOS app. <strong>Solution</strong>: <a href="https://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/free-provisioning/">this guide</a>.</li>
<li>Generic solution for many problems: restart Visual Studio (seriously, I've seen many StackOverflow questions where somebody was wondering why something does not work, and then "oh...after restarting Visual Studio it started working").</li>
</ul>
<p>One, not Xamarin specific tip: if want to have relations in SQLite database? Use <a href="https://bitbucket.org/twincoders/sqlite-net-extensions">SQLite-Net Extensions</a>.</p>
<h3>Publishing apps to stores</h3>
<p><strong>Android</strong> - bananas! Seconds for auto-validation, and ~3 hours to the store. I didn't encounter any problems except copyrights for Bread Crumbs app icon, which I had to change. It was automatically detected! Impressive! <a href="https://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/publishing_an_application/">This guide</a> is more than enough to guide you through the process.</p>
<p><strong>iOS</strong> - ~20 minutes for auto-validation, and ~4(!) days to the store. You can check current wait times <a href="http://appreviewtimes.com/">here</a>. Creating app bundle might be a little bit challenging. I was able to figure it out with <a href="https://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/app_distribution/app-store-distribution/publishing_to_the_app_store/">Xamarin guide</a> and <a href="https://gist.github.com/brendanzagaeski/9220557">this gist</a> (I recommend option 2).</p>
<p><strong>Windows Store</strong> - ~3h for auto-validation, and ~1 day to the store. I had my apps rejected, despite the fact that they were working on Windows machine, and on Windows Phone Device (Lumia 920). There were 2 issues:</p>
<ol>
<li>Referencing incorrect SQLite assembly: "SQLite for Universal <strong>App</strong> Platform" instead of "SQLite for Universal <strong>Windows</strong> Platform".</li>
<li>I didn't test apps with with .NET Native (Project properties &gt; Build &gt; Compile with .NET Native Tool Chain), and one app was crashing during verification process. After debugging with .NET Native I was able to repro, diagnose and fix the problem.</li>
</ol>
<h3>Summary</h3>
<p>Xamarin is not only sunshine and rainbows. You will have problems you wouldn't when developing native apps, but also - you do not have some problems you would have when developing native apps. Check discussion about pros and cons of using Xamarin at Hacker News: <a href="https://news.ycombinator.com/item?id=9320929">Some thoughts after (almost) a year of real Xamarin use</a>.</p>
<p>Be aware that there are also other cross-platform mobile frameworks, e.g., <a href="https://cordova.apache.org/">Apache Cordova</a>, <a href="https://facebook.github.io/react-native/">React Native</a>, or <a href="https://www.nativescript.org/">NativeScript</a> .</p>
<p>Since this year, Xamarin is <a href="https://store.xamarin.com/">free</a> for Students, OSS projects and <a href="https://www.visualstudio.com/support/legal/mt171547">small teams</a> (up to 5 people). You can use Visual Studio (including free Visual Studio Community Edition) or free Xamarin Studio Community Edition. That means - now you can use Xamarin for FREE!</p>
<p><iframe src="https://www.youtube.com/embed/fUXdNfAsCWg" width="640" height="360" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>Happy development!</p>
<p>Let me know in comments if you have any questions about developing apps with Xamarin!</p>

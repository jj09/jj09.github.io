---
layout: post
title: Dependency Injection in C# - 2017 update
date: 
type: post
parent_id: '0'
published: false
password: ''
status: draft
categories:
- programming
tags:
- C#
- Dependency Injection
- IoC
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
  _oembed_d5f52e9d4eb0080be4d381480bbc3dfe: "{{unknown}}"
  _oembed_6866cb5bea8aa53aed874752e88e0317: "{{unknown}}"
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/"
---
<p>"If your program is larger than 300 lines of code, you should use DI"</p>
<p>// IoC vs DI</p>
<p>//Dependency Injection in .NET (Mark Seemann)</p>
<p>//Mark articles: http://blog.ploeh.dk/2014/06/10/pure-di/</p>
<p>// poor man's DI -&gt; pure DI</p>
<p>// antipatterns</p>
<p>//ioc benchmark: http://www.palmmedia.de/blog/2011/8/30/ioc-container-benchmark-performance-comparison</p>
<p>//twitter poll results (send another pool with AutoFac, SimpleInjector, StructureMap and ...)</p>
<p>//main candidates:<br />
AutoFac<br />
SimpleInjector - nice API and fast<br />
MVVMCross baked in container<br />
StructureMap - oldest<br />
TinyIoC (no .NET Core, no WinRT?)<br />
Ninject (perf sucks)</p>
<p>https://github.com/jj09/DI</p>
<p>&nbsp;</p>
<p>// DI for Xamarin</p>
<p>&nbsp;</p>
<p>Choosing DI container xlsx</p>

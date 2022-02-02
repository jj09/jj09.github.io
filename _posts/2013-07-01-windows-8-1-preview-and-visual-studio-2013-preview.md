---
layout: post
title: Windows 8.1 Preview and Visual Studio 2013 Preview
date: 2013-07-01 09:48:55.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
- tools
tags:
- Open Source
- visual studio
- windows
- Windows 8
- Windows 8.1
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  dsq_thread_id: '1499386464'
  feature_size: blank
  builder_switch_frontend: '0'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/windows-8-1-preview-and-visual-studio-2013-preview/"
---
<p>At the <a href="http://www.buildwindows.com/">build conference</a> (June 26-28, 2013) Microsoft announced <a href="http://windows.microsoft.com/en-us/windows-8/preview-download">Windows 8.1 Preview</a> and <a href="http://www.microsoft.com/visualstudio/eng/2013-downloads">Visual Studio 2013 Preview</a>. I installed them on my Virtual Machine. Just in case, to protect my system from some unexpected features :)</p>
<p>In case of Windows 8.1 there are no big changes. Only some small, useful improvements. I like 'search all', which enables you to search within apps, settings and files in the same time. However I am still using <a href="http://www.voidtools.com/">Search Everything</a>, because it's faster and more effective. It's also cool to have the Start button, which brings you to the metro desktop, but again - no big deal (I was ok with WIN button). You can find list of improvements/changes <a href="http://www.extremetech.com/computing/159803-windows-8-1-a-complete-list-of-changes-and-new-features">here</a> and <a href="http://www.hanselman.com/blog/10NewFeaturesInWindows81PreviewThatSavedMySurfaceRT.aspx">here</a>.</p>
<p>The new Visual Studio is more interesting. The One ASP.NET idea is applied. When you create new project, there are only one template: 'ASP.NET Web Application'. Then in second step, you can choose which type<b>s</b> of application<b>s</b> you want to include into it.</p>
<div style="text-align: center;"><img class="alignnone size-medium wp-image-286" style="display: inline;" src="{{ site.baseurl }}/assets/2013/07/vs2013_oneaspnet.jpg" alt="Visual Studio 2013 One ASP.NET" width="500" /><img class="alignnone size-medium wp-image-287" style="display: inline;" src="{{ site.baseurl }}/assets/2013/07/vs2013_oneaspnet_templates.jpg" alt="Visual Studio 2013 One ASP.NET templates" width="400" /></p>
</div>
<p>There is MVC 5 (Preview) in it, along with various scaffolding options. You can e.g. scaffold just edit action.</p>
<p>Great feature for web developers: you can open page in multiple web browsers and then refresh them all from Visual Studio (e.g. after change in code).</p>
<p>The editors experience is improved. You can have code map in the scroll bar. HTML editor is rewritten from scratch. Short list of my favorite features:</p>
<ul>
<li>new code snippets (in HTML document try: 'div.myClass*4&gt;lorem' and click TAB)</li>
<li>intellisense in web.config</li>
<li>ALT + UP/DOWN - move code line up or down</li>
<li>ALT + 1/2 - extends text selection to level up or down</li>
<li>ALT+SHIFT+W - allows to surround selected text with new tag</li>
<li>ALT+V - voice commands (which shows shortcuts), yes we can speak to Visual Studio!</li>
<li>JavaScript frameworks intellisense (e.g. AngularJS)</li>
</ul>
<p>But the greatest news is: WebEssentials2013 are now Open Source on <a href="https://github.com/madskristensen/WebEssentials2013">github</a>. Everyone can contribute. The policy is to add experimental features to WebEssentials and then move the hottest to Visual Studio (once they are tested). To see all, new, hot features watch <a href="http://channel9.msdn.com/Events/Build/2013/3-503">Mads Kristensen's talk at build 2013</a>.</p>
<p>Another cool thing is possibility to 'sign in' in the Visual Studio. Once you sign in using your Microsoft account, you can synchronize settings across your devices. Now, it is enough to customize you Visual Studio only once.</p>
<p>There is much more new features. You can find them <a href="http://blogs.msdn.com/b/somasegar/archive/2013/06/26/visual-studio-2013-preview.aspx">here</a> and <a href="http://blogs.msdn.com/b/bharry/archive/2013/06/03/visual-studio-2013.aspx">here</a>.</p>

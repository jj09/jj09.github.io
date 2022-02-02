---
layout: post
title: Update to Windows 8.1 from Windows 8
date: 2014-01-08 15:36:38.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- tools
tags:
- PowerShell
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
  dsq_thread_id: '2100987820'
  feature_size: blank
  builder_switch_frontend: '0'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/update-to-windows-8-1-from-windows-8/"
---
<p>Before you decide to upgrade your Windows 8 to 8.1, you should be aware of some issues/changes.</p>
<p>To begin with, it is not very obvious and easy to find a way, to avoid using Microsoft Account. Fortunately, Scott Hanselman described it in his blog, in his post <a href="http://www.hanselman.com/blog/HowToSignIntoWindows8Or81WithoutAMicrosoftAccountMakeALocalUser.aspx">How to sign into Windows 8 or 8.1 without a Microsoft account - make a local user</a>.</p>
<p>Another issue is SkyDrive. If you are not using it, then you do not need to worry. But if you do (like me) then be aware that now it is integrated with Windows 8.1. You are not able to use SkyDrive app like in Windows 8. What is more: <span style="text-decoration: underline;">you need to sign in with Microsoft Account on Windows 8.1, to be able to use SkyDrive</span>. In the recent version of SkyDrive, Microsoft introduced "smart files". It distinguish two types of files: online-only (not stored on your hard drive and available when you are connected to the Internet) and offline (old-style files, can be used when you are offline and will be synced once you get online). Default status of new created file is online-only. You need to change it if you want to use files in the old-way (offline). There are two ways to do that. First: go to SkyDrive app and mark file/directory you want to make offline (by right click) and click "Make offline" in app bar:</p>
<p><img class="aligncenter size-full wp-image-820" src="{{ site.baseurl }}/assets/2014/01/SkyDrive-makeOffline.jpg" alt="SkyDrive - make offline" width="800" /></p>
<p>Second way is go to SkyDrive settings and set "Access all files offline" to "On":</p>
<p><img class="aligncenter size-full wp-image-823" src="{{ site.baseurl }}/assets/2014/01/SkyDrive-accessAllFilesOffline.jpg" alt="SkyDrive - access all files offline" width="346" height="267" /></p>
<p>You can find more details about "smart files" <a href="http://windows.microsoft.com/en-us/windows-8/skydrive-online-available-offline">here</a>.</p>
<p>All above issues are fixable. However there are a few things, which cannot be solved (so far). I have ThinkPad X220 (i5@2.3GHz, 8GB RAM, 160GB SSD) and I did a system upgrade from Win8 to Win8.1. Since then, the performance is a little bit worse. Additionally, I have two monitors connected through VGA and DisplayPort. The second monitor is all gray right after system boot. I need to click WIN+D to get the desktop. I do not have this issue on my PC where I installed Win 8.1 from scratch.</p>
<p>I use PowerShell as my default command line. There is a weird issue with Lucidia Console font on Windows 8.1. You cannot set it as default font. It is not a huge concern, because the Consolas works fine, but I cannot use Lucidia Console (which I like better). More about this issue <a href="http://superuser.com/questions/538607/cannot-change-powershell-default-font-to-lucida-console">here</a>.</p>
<p>Now, let's look at the bright side of life. My favorite Windows 8.1 feature is "search everywhere". You do not need to think whether you want to search programs (WIN+Q), settings (WIN+W) or files (WIN+F). However, <a href="http://www.voidtools.com/">Everything Search Engine</a> is still the best for searching files.</p>
<p>I like the Windows button too. After right-click, you have the same menu which you get with WIN+X. Furthermore, there are options shutdown/restart/sleep there. It is easier and faster accessible than "Mouse to right-bottom corner of screen"-&gt;Settings-&gt;Power-&gt;Shut down.</p>
<p>Another nice feature is the adjustable size of tiles:</p>
<p><img class="aligncenter size-full wp-image-834" src="{{ site.baseurl }}/assets/2014/01/Windows81-adjustableTiles.jpg" alt="Windows8.1 - adjustable tiles" width="513" height="260" /></p>
<p>To learn about other new features I recommend Scott Hanselman's <a href="http://www.hanselman.com/blog/ThreeAllNewWindows81VideoTutorialsWhatsNewIn81KeyboardShortcutsAndManagingWindows.aspx">videos about new features in Windows 8.1</a>. He is showing how to be productive on Windows 8.1 and how to take advantage of key shortcuts.</p>
<p><strong>By the way: <span style="font-size: 27px;">Happy New Year 2014!</span></strong></p>
<p><img class="aligncenter size-full wp-image-830" src="{{ site.baseurl }}/assets/2014/01/new-year-eve-fireworks-2014-new-york.jpg" alt="Happy New Year 2014" width="800" height="470" /></p>

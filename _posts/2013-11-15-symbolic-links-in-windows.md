---
layout: post
title: Symbolic Links in Windows
date: 2013-11-15 10:58:11.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- tools
tags:
- PowerShell
- terminal
- windows
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _syntaxhighlighter_encoded: '1'
  dsq_thread_id: '1968788036'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/symbolic-links-in-windows/"
---
<p>Since Windows Vista we have possibility to create symbolic links on Windows. Yay!</p>
<p>To do that, we have command <code>mklink</code> in Command Prompt:</p>
<p><code>C:\Users\jj\Desktop>mklink link_to_some_file.txt c:\Dropbox\some_file.txt<br />
symbolic link created for link_to_some_file.txt <<===>> c:\Dropbox\some_file.txt</code></p>
<p>Symbolic link is not a shortcut. However, its icon desktop looks the same:</p>
<p><img src="{{ site.baseurl }}/assets/2013/11/link_and_shortcut_icons.png" alt="link and shortcut icons in Windows" width="102" height="196" class="aligncenter size-full wp-image-790" /></p>
<p>You can find out whether it is a link or shortcut by looking on the properties (left - link, right - shortcut):</p>
<p><img src="{{ site.baseurl }}/assets/2013/11/link_vs_shortcut.png" alt="link vs shortcut in Windows" width="753" height="516" class="aligncenter size-full wp-image-791" /></p>
<p>You can also check it from the command prompt:<br />
<code>C:\Users\jj\Desktop>dir<br />
 Volume in drive C has no label.<br />
 Volume Serial Number is A425-1CEF</p>
<p> Directory of C:\Users\jj\Desktop</p>
<p>11/15/2013  10:36 AM    &lt;DIR>          .<br />
11/15/2013  10:36 AM    &lt;DIR>          ..<br />
11/15/2013  10:35 AM    &lt;SYMLINK>      link_to_some_file.txt [c 1="le.txt" language=":Dropboxsome_fi"][/c]<br />
11/15/2013  10:36 AM               921 some_file - Shortcut.lnk<br />
               2 File(s)            921 bytes<br />
               2 Dir(s)  15,738,155,008 bytes free<br />
</code></p>
<p>OT: Don't you think <code>dir</code> command is to verbose? Who needs e.g. Volume Serial Number each time during listing directory?</p>
<p>In PowerShell, you need to use following command: <code>cmd /c mklink</code> (precede <code>mklink</code> with <code>cmd /c</code>).</p>
<p>I use it for my <a href="http://jj09.net/windows-powershell-profile/" title="Windows PowerShell profile">PowerShell config file</a>. Original one is in Dropbox and symlink just point to it from MyDocuments directory (where it has to be, to be applied by PowerShell).</p>

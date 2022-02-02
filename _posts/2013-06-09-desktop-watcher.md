---
layout: post
title: Desktop Watcher
date: 2013-06-09 18:13:19.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- C#
- github
- Open Source
- WinForms
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _yoast_wpseo_metadesc: Program which detects mouse move and keyboard interaction
  dsq_thread_id: '1504402345'
  enclosure: |
    https://github.com/jj09/DesktopWatcher/blob/master/alarm.mp3
    24026
    audio/mpeg
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/desktop-watcher/"
---
<p>Have you ever forgotten to lock your computer and went for a lunch? If so then you know what can happen. Your coworkers can send invitation for a party at your place to all co-workers (using your e-mail). They can also mess up with your desktop icons and much, much other fun stuff. The best solution is always lock the system. However sometimes we forget about it.</p>
<p>Once I was bored after work I created WinForms application, which starts playing scary sound when somebody move the mouse or push some key on the keyboard (while I am out of my desk). Usually when you want to mess up with somebody's machine your heart rate is higher than normal (because of adrenaline that you can be caught). Then not expected scary sound can cause even heart attack.</p>
<p>I named my app: Desktop Watcher. It looks like that:</p>
<p><img class="alignnone size-full wp-image-65" alt="Desktop Watcher" src="{{ site.baseurl }}/assets/2013/06/DesktopWatcher.jpg" width="139" height="82" /></p>
<p>When you hit <em>Play</em>, you get file dialog to choose some scary sound (<a href="https://github.com/jj09/DesktopWatcher/blob/master/alarm.mp3">like this</a>) from your hard drive. Then you need to put cursor in the program area and leave your machine. You have 5 seconds for that. Every mouse move or keyboard's key push after that will start sound playing and lock the machine. If you caught somebody the machine will be locked and sound will be playing. To quit the app you need to unlock the machine and hit ALT-F4  immediately (two keys together - because hit only ALT will cause lock screen again) or close app by mouse if you are quick hand person.</p>
<p>No worries that somebody close your app by ALT-F4 before he moves the mouse. If so then system will be locked anyway (but no sound will be played). You do not need to worry about it, because it means that somebody knew you prepared a trap :)</p>
<p>There is an issue that mouse needs to be in the program area to detect mouse moves. I may fix it in the future, but for now you can just hide the app somewhere (e.g. on right bottom corner):</p>
<p><img class="alignnone size-medium wp-image-66" alt="Desktop Watcher hidden" src="{{ site.baseurl }}/assets/2013/06/DesktopWatcher_hidden-300x140.jpg" width="300" height="140" /></p>
<p>Source (and sample scary sound) is available on github: <a href="https://github.com/jj09/DesktopWatcher">https://github.com/jj09/DesktopWatcher</a>.</p>

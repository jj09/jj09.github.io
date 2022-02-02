---
layout: post
title: Windows 10 on VirtualBox - resolution problem
date: 2014-12-17 18:54:09.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- other
tags:
- VirtualBox
- Windows 10
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
  dsq_thread_id: '3335264993'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/windows-10-virtualbox-resolution-problem/"
---
<p>If you are running Windows 10 on VirtualBox you may experience limited resolutions availability.</p>
<p>To solve this problem, you can add <em>CustomVideoMode</em> (VirtualBox has to be closed at this time):</p>
<p><code>.\VBoxManage.exe setextradata "VM-Name" CustomVideoMode1 1600x900x32</code></p>
<p>To confirm it is set, use <em>getextradata</em> command:</p>
<p><code>.\VBoxManage.exe getextradata "Win10" CustomVideoMode1</code></p>
<p>Or list all settings:</p>
<p><code>.\VBoxManage.exe getextradata "Win10" enumerate</code></p>
<p><img class="alignnone size-full wp-image-7601" src="{{ site.baseurl }}/assets/2014/12/VirtualBoxCommands.png" alt="VirtualBox commands" width="683" height="315" /></p>
<p>Remember that VirtualBox has to be closed at the time when you execute these commands. If everything went smoothly, you should see new resolution after Virtual Machine restart:</p>
<p><img class="alignnone size-full wp-image-7611" src="{{ site.baseurl }}/assets/2014/12/win10-resolutions-onVB.png" alt="Windows 10 resolutions on VirtualBox" width="538" height="571" /></p>
<p>&nbsp;</p>
<p>* This might be also an issue with other versions of Windows.</p>

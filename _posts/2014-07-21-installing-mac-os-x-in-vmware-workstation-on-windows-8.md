---
layout: post
title: Installing Mac OS X in VMWare Workstation on Windows 8
date: 2014-07-21 09:04:26.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- other
tags:
- macos
- windows
- Windows 8
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
  dsq_thread_id: '2861193491'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/installing-mac-os-x-in-vmware-workstation-on-windows-8/"
---
<p>I created Mac OS X Virtual Machine on VMWare. It wasn't simple process, so I decided to share this experience. I was following <a href="http://myitforum.com/myitforumwp/2013/06/07/running-mac-os-x-on-windows-vmware-workstation/">this</a> article. Here is an outline:</p>
<ol>
<li>Download and install <a href="http://www.vmware.com/products/workstation/">VMWare Workstation</a>. But to do that, you need to <a href="http://winquire.org/2012/06/26/install-both-hyper-v-and-vmware-workstation-on-windows-8-without-errors/">disable Hyper-V</a> first.</li>
<li>Download <a href="http://www.insanelymac.com/forum/files/file/20-vmware-unlocker-for-os-x/">VMWare unlocker</a> and run windows/install.cmd script. It allows to choose Mac OS X system during VM creation later on.</li>
<li>Convert Mac OS X image (Mountain Lion in my case) from .dmg to .iso (using <a href="http://vu1tur.eu.org/tools/">dmg2img</a>).</li>
<li>Create VM for Mac OS X and choose created Mac OS X .iso file in new VM settings -&gt; hardware -&gt; CD/DVD (SATA) -&gt; Use ISO image file</li>
<li>Run Virtual Machine and install Mac OS X (described in <a href="http://myitforum.com/myitforumwp/2013/06/07/running-mac-os-x-on-windows-vmware-workstation/">mentioned</a> article).</li>
<li>Install <a href="http://softwareupdate.vmware.com/cds/vmw-desktop/fusion/6.0.4/1887983/packages/com.vmware.fusion.tools.darwin.zip.tar">VMWare tools</a> (also described in <a href="http://myitforum.com/myitforumwp/2013/06/07/running-mac-os-x-on-windows-vmware-workstation/">mentioned</a> article).</li>
</ol>
<p>Once Mac OS X is installed and running I updated Mountain Lion to Mavericks. That was easy and went smoothly. Additionally I recommend to do following:</p>
<ol>
<li><a href="https://www.vmware.com/support/ws5/doc/ws_running_shared_folders.html">Enable shared folders</a> (they are located in /Volumes/VMWare Shared Folders/NAME_OF_FOLDER)</li>
<li>Install <a href="http://totalfinder.binaryage.com/">TotalFinder</a></li>
<li>Install <a href="http://www.iterm2.com">iTerm 2</a></li>
<li>Install <a href="http://manytricks.com/witch/">Witch</a></li>
<li>Install <a href="http://www.sublimetext.com/3">SublimeText 3</a></li>
<li>Install <a href="https://developer.apple.com/xcode/downloads/">Xcode</a> (not only for iOS development, it contains e.g. gcc compiler)</li>
</ol>
<p>Linux (Ubuntu) installation is much easier. You just download <a href="http://www.ubuntu.com/download">Ubuntu iso</a> and <a href="http://betanews.com/2012/08/29/how-to-install-ubuntu-on-vmware-workstation/">create VM on VMWare workstation</a> using downloaded .iso file. That's it.</p>

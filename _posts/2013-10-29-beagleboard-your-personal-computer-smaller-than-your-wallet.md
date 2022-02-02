---
layout: post
title: BeagleBoard - your personal computer smaller than your wallet
date: 2013-10-29 17:20:46.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- hadrware
- programming
tags:
- Ada
- BeagleBoard
- Java
- linux
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
  dsq_thread_id: '1916304310'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/beagleboard-your-personal-computer-smaller-than-your-wallet/"
---
<p><img src="{{ site.baseurl }}/assets/2013/10/beagleboard_xm.jpg" alt="BeagleBoard XM" width="252" height="252" class="aligncenter size-full wp-image-755" /></p>
<p>It is amazing how big progress was made in embedded systems recently. I remember when I had microcontrollers class at Wroclaw University of Technology (about 3 years ago) and we were programming in Assembly. When I heard (3 years ago) that the main language for programming microcontrollers is C++ I was so excited. It would be so much easier than in Assembly. Now (3 years later), I started working on my Master Thesis at Kansas State University. The ultimate goal is to create prototype of medical device using embedded computer <a href="http://beagleboard.org/Products/BeagleBoard-xM">BeagleBoard XM</a>.</p>
<p>This board has 1GHz ARM processor (Cortex-A8), 512MB RAM, 4 USB ports and even HDMI output. Moreover, it has MicroSD slot which allows you to run Linux or Android Operating system!</p>
<p><img src="{{ site.baseurl }}/assets/2013/10/shocked.gif" alt="shocked" width="463" height="259" class="aligncenter size-full wp-image-753" /></p>
<p>There is also Ethernet port, which allows to update the Operating System without any external PC. The key part of the device is set of <a href="http://en.wikipedia.org/wiki/Pulse-width_modulation">PWM</a> pins, which will allow me to control the medical device engine.</p>
<p>I will use Ada programming language with <a href="http://www.embedded-news.tv/component/resource/article/1-all-videos/519">cross-compiler from AdaCore</a>. However you can install Java VM and run Java programs if you want! It blows my mind! Programming microcontrollers in Java (the very high-level programming language) instead of doing it in Assembly.</p>
<p>The cost of this Board is $149, which is another advantage of this device.</p>
<p>More info about the board can be found <a href="http://beagleboard.org/Products/BeagleBoard-xM">here</a>.<br />
It usually comes along with MicroSD card and Angstrom Linux on it. Additionally, you can find Angstrom images <a href="http://angstrom.s3.amazonaws.com/demo/beagleboard/index.html">here</a>. To update existing installation (of Angstrom) just do </p>
<p><code>opkg update<br />
opkg upgrade</code></p>
<p>More info about OPKG Package Manager (Angstrom's Package Manager) can be found <a href="http://wiki.openwrt.org/doc/techref/opkg">here</a>.</p>

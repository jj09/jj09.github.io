---
layout: post
title: FreeRTOS Jump Start
date: 2014-04-17 11:03:58.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- hadrware
- programming
tags:
- C#
- FreeRTOS
- TivaWare
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  dsq_thread_id: '2619218643'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/freertos-jump-start/"
---
<p>In this semester I am taking Real-Time Systems course. In one of the programming assignments, we had to develop program for embedded device <a href="http://www.ti.com/tool/ek-tm4c123gxl">Tiva C Series LaunchPad TM4C123G</a>. It is a low-cost evaluation platform for ARM Cortex-based microcontrollers from Texas Instruments. It is very nice board if you want to start with embedded devices. It cost only <a href="http://www.ebay.com/itm/TI-Cortex-M4-EK-TM4C123GXL-TM4C123G-LaunchPad-Evaluation-Board-/181298354391">$25 on eBay</a>. You can connect it to your computer using USB. Finally, the board has key feature of embedded device for beginners: the LED. </p>
<p><img src="{{ site.baseurl }}/assets/2014/04/TITivaLaunchpad.jpg" alt="Tiva LaunchPad" width="250" class="aligncenter size-full wp-image-1272" /></p>
<p>A typical process-control system can be divided into four types of components: the process, sensors, actuators, and controller (see Figure below). LED allows you to mock your target actuator. Majority of operations performed by embedded devices is control of the actuators. What is nice about LED: it is cheap and easy to control whether and how it is working.</p>
<p><img src="{{ site.baseurl }}/assets/2014/04/safety-critical-loop.gif" alt="safety critical loop" width="540" height="297" class="aligncenter size-full wp-image-1274" /></p>
<h3>Code Composer Studio</h3>
<p>As a development environment for Tiva C Series I recommend you <a href="http://www.ti.com/tool/ccstudio">Code Composer Studio</a>. It is Eclipse based IDE, which makes development easy. Especially for beginners. Tutorial for installation and running first program on Tiva TM4C123G board using Code Composer Studio can be found <a href="http://processors.wiki.ti.com/index.php/Tiva_TM4C123G_LaunchPad_Blink_the_RGB">here</a>. I recommend to follow the "Single Download" option (download 1GB+ file). More precisely, download and install: "EK-TM4C123GXL-CCS: TivaWare for C Series and Code Composer Studio for the Tiva C Series TM4C123G LaunchPad" <a href="http://www.ti.com/tool/sw-ek-tm4c123gxl">available on this website</a>. I wasted a lot of time trying to install it following "Individual Downloads" instructions (download <1MB file). Installer was hanging, when it was downloading files form the Internet and never recovers. In "Single Download" most of files are already downloaded along with the installer.</p>
<h3>FreeRTOS</h3>
<p>FreeRTOS is one of the most popular Real Time Operating Systems (RTOS). Additionally, it is free. This is where its name comes from (<b>free</b> + <b>R</b>eal <b>T</b>ime <b>O</b>perating <b>S</b>ystem = FreeRTOS). The System is written in C language. Thus, we write programs for it in C as well. More details can be found on <a href="http://www.freertos.org/">freertos.org</a> and <a href="http://en.wikipedia.org/wiki/FreeRTOS">wikipedia</a>.</p>
<p>The cool thing about FreeRTOS is that it enables easy modifications of Operating System. You can modify e.g. scheduler.</p>
<p>Once you have Code Composer installed. You need to install TivaWare software (which includes FreeRTOS). It can be found in previously downloaded package (if you were following "Single download" option) in TivaWare/SW-EK-TM4C123GXL-1.1.exe.</p>
<h3>Running example programs</h3>
<p>The TivaWare software contains examples, which are ready to run. You can find them in the directory, where you installed TivaWare C Series software. In my case (default path) it is: <code>C:\ti\TivaWare_C_Series-1.1\examples</code>.</p>
<p>There is an example project freertos_demo. It makes the LED blinking and allows you to manipulate the colors using buttons (located at the bottom of the board). The project can be found in <code>examples\boards\ek-tm4c123gxl\freertos_demo</code>. It is ready to run. You just need to connect the board to the PC, open the project (import it) in Code Composer Studio and run it in debug mode. Code Composer Studio will automatically port the program into the board.</p>
<p>You can modify the code, and make the LED blinking faster or slower. Colors manipulation is also easy.</p>
<h3>Queues and semaphores</h3>
<p>FreeRTOS supports multitasking. In the Real-Time systems, communication between different tasks are usually implemented using queues and semaphores. It is also the case in freertos_demo program. Buttons send messages to the LED using queues. Semaphores are use to guard concurrent access to <a href="http://en.wikipedia.org/wiki/Universal_asynchronous_receiver/transmitter">UART</a>. </p>
<p><a href="http://www.socialledge.com/sjsu/index.php?title=FreeRTOS_Tutorial">This tutorial</a> is very good point to start with FreeRTOS. It describes basics, queues, semaphores and more.</p>
<h3>Summary</h3>
<p>Developing code for embedded devices is usually, more complex than for Web or Desktop. Running, even very simple application is more complex, because it requires more steps. You need to configure connection between your computer/OS and specific device. Then you need to setup many settings, which varies almost among every device. The communication with ports is also different and every device has different set of them.</p>
<p>There are no universal installers etc. Every single device require slightly different setup. Sometimes, you need to spend hours to run simple "Hello, World!" application. On the other hand, it is fun to create some system, which do stuff outside of your PC.</p>
<p>If you are interested in embedded devices, check out my other post: <a href="http://jj09.net/beagleboard-your-personal-computer-smaller-than-your-wallet/">BeagleBoard - your personal computer smaller than your wallet</a>.</p>
<p>To get started with FreeRTOS and Tiva C Series: check <a href="http://processors.wiki.ti.com/index.php/Tiva_TM4C123G_LaunchPad_Blink_the_RGB">this tutorial</a> to run first program and <a href="http://www.socialledge.com/sjsu/index.php?title=FreeRTOS_Tutorial">FreeRTOS Tutorial</a> to get more details. You can buy <a href="http://www.ebay.com/itm/TI-Cortex-M4-EK-TM4C123GXL-TM4C123G-LaunchPad-Evaluation-Board-/181298354391">Tiva C Series LaunchPad on eBay</a>.</p>

---
layout: post
title: Solution for missing battery icon on Surface Book running Windows 10
date: 2019-04-23 13:15:04.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- hadrware
tags:
- surfacebook
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
  dsq_thread_id: '7376372999'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/solution-for-missing-battery-icon-on-surface-book-running-windows-10/"
---
<p>Recently I got a Surface Book 2. From the beginning, my battery icon was missing, and I spent hours researching how to fix it. I didn't even have battery show up in device manager.</p>
<p>To save you hours, here is the solution:</p>
<ol>
<li>Go to device manager</li>
<li>View -&gt; show hidden devices<br />
<img class="aligncenter size-full wp-image-19746" src="{{ site.baseurl }}/assets/2019/04/missing-batter-icon-device-manager-show-hidden-devices.jpg" alt="Missing battery icon on Surface Book" width="600" height="317" /></li>
<li>Uninstall <strong>Surface Serial Hub Driver</strong>:<br />
<img class="aligncenter size-full wp-image-19747" src="{{ site.baseurl }}/assets/2019/04/missing-batter-icon-device-manager-uninstall-surface-serial-hub-driver.jpg" alt="Missing Battery Icon on Surface Book - uninstall Surface Serial Hub Driver" width="674" height="460" /></li>
<li>uninstall all other devices that have warnings*</li>
<li>reboot and wait a few minutes for missing drivers to get reinstalled</li>
</ol>
<p>(*) - I am not 100% sure step 4 is required, but it won't hurt and it may help.</p>
<p>After that you should get your battery status back:</p>
<p><img class="aligncenter size-full wp-image-19748" src="{{ site.baseurl }}/assets/2019/04/surface-book-battery.jpg" alt="Surface Book - battery status" width="600" height="647" /></p>
<p>It should also be visible in device manager now:</p>
<p><img class="aligncenter size-full wp-image-19749" src="{{ site.baseurl }}/assets/2019/04/surfacebook-device-manager-battery.jpg" alt="Surface Book device manager - battery status" width="770" height="477" /></p>
<p>&nbsp;</p>

---
layout: post
title: MacBook External Display resolution problem
date: 2014-06-09 16:04:57.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- hadrware
tags:
- macbook
- macos
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
  dsq_thread_id: '2751472079'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/macbook-external-display-resolution-problem/"
---
<p><img class="aligncenter size-full wp-image-2501" src="{{ site.baseurl }}/assets/2014/06/mac-3-monitors.png" alt="MacBook 3 monitors" width="800" height="330" /></p>
<p>Today I wasted 2 hours trying to adjust resolution on external monitor connected to my MacBook.</p>
<p>I work with two external Monitors (Sun 24"). One through miniDP/VGA, second: through USB/DVI.</p>
<p>Yesterday, I connected MacBook to 42" TV, with miniDP/VGA port. Today I connected it with Sun Monitor as usual and...I got black screen. I tried to change resolution, but...1920x1200, which I am usually working with, was not available. Even more: when I set 'Best for display' I got 800x640! Maximum available was 1600x1200, but it was wrong ratio! The Sun 24" monitor has 16:10 ratio, not 4:3!</p>
<p>I tried <a href="https://discussions.apple.com/message/23450245#23450245">deleting preferences, reseting PRAM etc.</a> It didn't help. Finally I tried to use miniDP/DVI (instead of miniDP/VGA) and I got 1920x1200. Then, when I connected miniDP/VGA again, I got 1920x1200 as well.</p>
<p>What I did wrong? I connected it when MacBook was in sleep mode. That is most likely cause of the issue. Probably MacBook thought it is still connected to 42" TV. Thus, changing port helped. Probably, if I connect it to another device, it would help as well.</p>
<p>In the past I already had issues when I was disconnecting monitors in sleep mode. Since that time, I was always connecting/disconnecting displays when MacBook was on. Except today :)</p>

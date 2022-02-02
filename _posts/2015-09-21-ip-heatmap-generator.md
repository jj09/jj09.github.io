---
layout: post
title: IP heatmap generator
date: 2015-09-21 21:28:01.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- javascript
- node
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
  dsq_thread_id: '4153064223'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/ip-heatmap-generator/"
---
<p><img class="aligncenter size-full wp-image-11321" src="{{ site.baseurl }}/assets/2015/09/ipheatmapgenerator.jpg" alt="IP heatmap generator" width="800" height="419" /></p>
<p>Recently, we were looking at the error logs of the Azure Portal. One of our ideas - in order to investigate errors that were hard to diagnose - was to check in which part of the World users who get errors are located. The assumption was that people from, e.g., New Zealand might have slow connection issues (timeouts) more likely than people from USA or Europe. I couldn't find any tool that does that, so I put a simple website at <a href="http://ipheatmap.azurewebsites.net/ipinfo.html">ipheatmap.azurewebsites.net</a>. The main page use <a href="https://www.npmjs.com/package/geoip-lite">geoip-lite</a> node library to geolocate IP address. For cross-check, you go to <a href="http://ipheatmap.azurewebsites.net/ipinfo.html">ipheatmap.azurewebsites.net/ipinfo.html</a>, and the IP will be located using <a href="http://ipinfo.io">ipinfo.io</a> API.</p>
<p>Creating website + setting up deployment from github took me less than 5 minutes on Azure. I didn't have to do any special configuration to get it work. I didn't even have to leave the Azure Portal to lookup github url, because it fetches all available repos automatically after you provide your credentials. Even better: repos are sorted by creation date - thus the recently created repo (one that you would choose most likely) is on top of the list.</p>
<p>Source code is available on github: <a href="https://github.com/jj09/ip-heatmap-generator">https://github.com/jj09/ip-heatmap-generator</a>.</p>

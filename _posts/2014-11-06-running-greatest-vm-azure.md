---
layout: post
title: Running the greatest VM on Azure
date: 2014-11-06 21:46:18.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- Azure
- cloud
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
  dsq_thread_id: '3200502764'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/running-greatest-vm-azure/"
---
<p>Recently Microsoft Azure introduced the <a href="http://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/">New D-Series Virtual Machine Sizes</a>. The "greatest" available VM has 16 cores, and 112 GB RAM. In my imagination it looks like that:</p>
<p><img class="aligncenter size-full wp-image-6261" src="{{ site.baseurl }}/assets/2014/11/superPC.jpg" alt="super PC" width="245" height="347" /></p>
<p>I thought it would be cool to create one, and play with it for a while. Not for a month, because that would cost almost $1000 (~700-800 EURO):</p>
<p><img class="aligncenter size-full wp-image-6421" src="{{ site.baseurl }}/assets/2014/11/hugevm-pricing.jpg" alt="Azure VMs pricing" width="800" height="445" /></p>
<p>However, what is cool about Azure - you can scale VM down when you are not using it. Even to the cheapest option - A0 Basic (~10 EURO / month). And using D14 for an hour cost only ~1 Euro.</p>
<p>When I was wondering which OS install on the VM I found that Azure already offers Windows 10 preview VM:</p>
<p><img class="aligncenter size-full wp-image-6291" src="{{ site.baseurl }}/assets/2014/11/azure-win10vm.jpg" alt="Azure Windows 10 VM" width="800" height="589" /></p>
<p>&nbsp;</p>
<p>This is how it looks after installation:</p>
<p><img class="aligncenter size-full wp-image-6301" src="{{ site.baseurl }}/assets/2014/11/hugevm.jpg" alt="Huge VM" width="800" height="504" /></p>
<p>Working on this VM was even better (faster) than on my PC at work (Xeon with 6 cores and 32GB RAM). To stress the VM I opened over 100 instances of Visual Studio:</p>
<p><img class="aligncenter size-full wp-image-6351" src="{{ site.baseurl }}/assets/2014/11/100vsonhugevm.jpg" alt="100 Visual Studios on Azure VM" width="800" height="450" /></p>
<p>After opening 90 instances the VM slowed down. I opened 103 Visual Studios in total, and VM didn't crash.</p>
<p>This feeling of having the most powerful machine I have ever work on is amazing. Even though it is virtual. The most amazing thing is the fact that it cost me only 1 Euro to play with it for an hour. I can get it in a few minutes, and get rid of it within seconds.</p>
<p>I am using it from time to time as my playground, and scale-up/down according to my needs.</p>
<p>Later in this year, the <a href="http://azure.microsoft.com/blog/2014/10/20/azures-getting-bigger-faster-and-more-open/">G-series of VMs will be available on Azure</a>. The biggest in this series would be G5: 32 Cores + 448 GB RAM. That's gonna be...awesome!</p>
<p><img class="aligncenter size-full wp-image-6331" src="{{ site.baseurl }}/assets/2014/11/happy.gif" alt="happy" width="330" height="427" /></p>

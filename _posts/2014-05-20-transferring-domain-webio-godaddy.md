---
layout: post
title: Transferring domain (from Webio to GoDaddy)
date: 2014-05-20 11:20:38.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- books
tags:
- domains
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
  dsq_thread_id: '2699994042'
  _wp_old_slug: transfering-domain-webio-godaddy
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/transferring-domain-webio-godaddy/"
---
<p>Recently, <a title="New domains" href="http://jj09.net/new-domains/">I purchased new domains at GoDaddy</a>. I decided to transfer my existing domain <a href="http://jj09.net">jj09.net</a> to GoDaddy as well. I thought it would be easy. However, I have never done this before.</p>
<p>Making long story short, here are steps to accomplish the transfer:</p>
<ol>
<li>Request the current registrar (in my case: <a href="https://www.webio.pl/">Webio</a>) to remove Privacy Protection and Theft Protection</li>
<li>Request the current registrar (in my case: <a href="https://www.webio.pl/">Webio</a>) to give you authinfo code</li>
<li><a href="http://support.godaddy.com/help/article/1592/transferring-domain-names-to-us?pc_split_value=2">Start domain transfer at GoDaddy</a></li>
<li>You should receive Transaction ID and Security code from the current registrar (requested by GoDaddy)</li>
<li>Authorize transfer at GoDaddy using:
<ul>
<li>Transaction ID</li>
<li>Security Code</li>
<li>Authinfo code</li>
</ul>
</li>
</ol>
<p>After that it should take around 7 days to perform the transfer. I received e-mail (from current registrar) that the transfer will be performed in a few days if I do not cancel it. It is some sort of theft protection. In your case (if you have different registrar) it may be different. E.g. you may need to confirm the transfer.</p>
<p>The best way is to contact you current registrar and destination registrar about the specific instructions. That's what I did and both was very nice and helpful.</p>
<p><strong>EDIT: </strong>Do not forget to change Nameservers and DNSes on GoDaddy after transfer is completed ;)</p>

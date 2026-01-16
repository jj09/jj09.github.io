---
layout: post
title: Taking Wordpress blog to HTTPS with CloudFlare in less than 10 minutes!
date: 2017-07-20 08:12:06.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- blog
- programming
- security
tags:
- https
- ssl
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
  dsq_thread_id: '6002569513'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/taking-wordpress-blog-to-https-with-cloudflare-in-less-than-10-minutes/"
image: /assets/2017/07/Cloudflare-e1500656493331.png
---
<p><img class="aligncenter size-full wp-image-18523" src="{{ site.baseurl }}/assets/2017/07/Cloudflare-e1500656493331.png" alt="CloudFlare" width="800" height="273" /></p>
<p>Making your website secure has never been easier! I was able to take my WordPress blog to HTTPS in less than 10 minutes!</p>
<h3>CloudFlare</h3>
<p>This part is super easy and straight-forward. Just sign up for <a href="https://www.cloudflare.com/">CloudFlare</a>, go to <a href="https://www.cloudflare.com/a/add-site">cloudflare.com/a/add-site</a> and follow instructions. You can also check <a href="https://www.youtube.com/watch?v=vbHN2sk3JjQ&amp;feature=youtu.be&amp;t=2774">this Troy Hunt's demo</a> to see it in action.</p>
<p>Once you finish, your website will be running on HTTPS!</p>
<p>Additional benefit is taking advantage of CloudFlare cache! For free! As you can see on the below screenshot, in last month: 54/66 GB was served from CloudFlare, only 11/66 GB came from my server!</p>
<p><img class="aligncenter size-full wp-image-18503" src="{{ site.baseurl }}/assets/2017/07/CloudFlare-Bandwidth-e1500656134409.png" alt="CloudFlare - cached bandwidth" width="800" height="607" /></p>
<h3>WordPress</h3>
<p>If you have WordPress blog (like I do), above setup will take your website to HTTPS, but all urls (hyperlinks, images, stylesheets etc.) will be still HTTP. This will result in <a href="https://developers.google.com/web/fundamentals/security/prevent-mixed-content/fixing-mixed-content">mixed content error</a>.</p>
<p>I love WordPress because every problem you may have was already solved by somebody else :) In this case problem is solved by <a href="https://jonnyjordan.com/blog/how-to-setup-cloudflare-flexible-ssl-for-wordpress/">CloudFlare Flexible SSL Plugin</a>.</p>
<h3>Multiple domains</h3>
<p>If you have multiple domains pointing to your blog, things are a little bit more complicated: <a href="http://www.itworld.com/article/2936598/servers/wordpress-multisite-ssl-with-domain-mapping-using-cloudflare.html">Wordpress Multisite SSL with domain mapping using Cloudflare </a>.</p>
<h3>Summary</h3>
<p>If you want to learn more about HTTPS, check out <a href="https://www.troyhunt.com/new-pluralsight-course-what-every-developer-must-know-about-https/">What Every Developer Must Know About HTTPS</a>. It is also worth to remember that <a href="https://www.troyhunt.com/i-wanna-go-fast-https-massive-speed-advantage/">HTTPS might be faster than HTTP</a>!</p>
<p>Is your website secure? Why not?</p>

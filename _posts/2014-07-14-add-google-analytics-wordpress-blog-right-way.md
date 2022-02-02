---
layout: post
title: How to add Google Analytics to Wordpress blog in the right way
date: 2014-07-14 16:19:14.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- blog
tags:
- Google Analytics
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
  dsq_thread_id: '2843724920'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/add-google-analytics-wordpress-blog-right-way/"
---
<p>I just found out, that Google Analytics was not counting my blog post pages. Only index page and all other subpages, but not post pages. This pages, which I am linking e.g. on twitter every time I blog!</p>
<p>From some time I was wondering if really only ~10 people are reading my blog. My last post about <a title="Getting started with iOS Development" href="http://jj09.net/getting-started-ios-development/">Getting started with iOS</a>, was visited by 12 people in the day it was published and 10 in the day after.</p>
<p><img class="aligncenter size-full wp-image-3471" src="{{ site.baseurl }}/assets/2014/07/ios-post-stats.png" alt="iOS post stats" width="886" height="232" /></p>
<p>Then, on Google Analytics, I went to behavior &gt; 'site content' &gt; 'all pages' to check how many people visited the blog post page. And...there are no post pages in the statistics at all!</p>
<p><img class="aligncenter size-full wp-image-3481" src="{{ site.baseurl }}/assets/2014/07/ios-post-stats-pages.png" alt="iOS post stats: pages" width="910" height="628" /></p>
<p>I knew that it is impossible, because at least I visited the post page. Then I checked statistics on Azure:</p>
<p><img class="aligncenter size-full wp-image-3491" src="{{ site.baseurl }}/assets/2014/07/ios-post-stats-azure.png" alt="iOS post stats: Azure" width="716" height="262" /></p>
<p>There are no unique views, but even page views on Google Analytics shows less than 20 per day. I published the post around 11 am, and announced it on twitter 11:18am. Then I got 7030 requests between 12pm and 1pm. It makes sense. Of course 1 Azure request &lt; 1 unique page view. According to Azure Management portal I had 62226 request in last week. How many unique pages views it is? I don't know and I will never know. But I am sure it is more than 54!</p>
<p>Why Google Analytics didn't track my posts? I put Google Analytics script in index.php file, in my Wordpress theme directory. Apparently I forgot to check if it works for all pages.</p>
<p>Now, I installed <a href="http://wordpress.org/plugins/insert-headers-and-footers/">Insert Headers and Footers</a> plugin to insert script from Google. As recommended in <a href="http://www.wpbeginner.com/beginners-guide/how-to-install-google-analytics-in-wordpress/">How to Install Google Analytics in WordPress for Beginners</a>. It seems to be working fine now. Here are statistics from today:</p>
<p><img class="aligncenter size-full wp-image-3501" src="{{ site.baseurl }}/assets/2014/07/ios-post-stats-pages-after.png" alt="iOS post stats: after Google Analytics script fix" width="905" height="331" /></p>
<p>There are also other plugins like <a href="https://wordpress.org/plugins/google-analytics-for-wordpress/">Google Analytics for WordPress</a> or <a href="https://wordpress.org/plugins/google-analyticator/">Google Analyticator</a>, but they insert Google Analytics snippet based on communication with Google api. It means, that if Google change their API for Google Analytics, plugin may not work. I don't want to be depend on that and just want to paste customized JS code I obtained from Google.</p>
<p>I also added Azure analytics script. Now, I will be able to cross-check the statistics.</p>

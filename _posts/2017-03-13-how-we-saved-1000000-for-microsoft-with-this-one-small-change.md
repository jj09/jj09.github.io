---
layout: post
title: How we saved $1,000,000 for Microsoft with this one, small change
date: 2017-03-13 22:10:20.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- Microsoft
- MSBuild
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
  dsq_thread_id: '5630477901'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/how-we-saved-1000000-for-microsoft-with-this-one-small-change/"
---
<p><img class="aligncenter size-full wp-image-14611" src="{{ site.baseurl }}/assets/2017/03/british_cycling_olympic_2012.jpg" alt="British Cycling Team - 2012 Olympics" width="636" height="464" /></p>
<p>Everyday when I am doing some small bug fixes or minor improvements I am thinking about the British Cycling team. They dominated 2012 Olympics thanks to <a href="http://www.bbc.com/sport/olympics/19174302">marginal improvements</a>. Such as cleaning hands properly, taking their own pillows when traveling or sleeping in the right position. All of these small things put together resulted in 7 out of 10 track cycling gold medals.</p>
<p>It turns out that the same strategy might work in software development. Especially if you work on large project.</p>
<h3>1 million dollar improvement</h3>
<p>In Azure Portal we have hundreds of developers working on one codebase. We are using <a href="https://github.com/Microsoft/msbuild">MSBuild </a>to perform builds. With default options, MSBuild was printing out to console a lot of logs that weren't very useful. When you are building project, you are usually interested in errors. It turned out that changing verbosity of output speed up builds from a few seconds to a few minutes depending on the project that is being built and type of the build (incremental / rebuild all).</p>
<p>Taking into account that there is at least 100 developers working everyday on the Azure Portal (in fact there is much more, but not everybody is working on the Portal full time), and assuming that everybody is performing at least 20 builds per day (savings up to 30 seconds per build), and 4-5 full project builds (savings around 1-2 minutes), every developer can save around 20 minutes everyday!</p>
<p>This gives us:</p>
<p><strong>100</strong> developers x <strong>20</strong> minutes x <a href="http://www.calendar-12.com/working_days/2016"><strong>240</strong> days working days per year</a> = <strong>480,000</strong> minutes = <strong>8,000</strong> hours</p>
<p>Assuming ~<strong>$150</strong>/hr  it give us total savings: <strong>8000</strong>*<strong>$150</strong> = <strong>$1,200,000</strong></p>
<h3>Incremental changes over years</h3>
<p>When I am looking back, I am impressed how much the Azure Portal have changed over last two years. This is portal in 2014:</p>
<p><img class="aligncenter size-full wp-image-14631" src="{{ site.baseurl }}/assets/2017/03/azure-portal-2014.png" alt="Azure Portal in 2014" width="800" height="468" /></p>
<p>This is portal in 2017:</p>
<p><img class="aligncenter size-full wp-image-14641" src="{{ site.baseurl }}/assets/2017/03/azure-portal-2016.png" alt="Azure Portal in 2016" width="800" height="444" /></p>
<p>We haven't done any breakthrough changes overnight. I have never had a feeling that one day resulted in some significant difference. It was 1 step at the time, one small bug fix one day, one tiny part of new feature another day.</p>
<h3>Small improvements every day, everywhere...</h3>
<p>This applies not only to large scale project. Think about Open Source. Even when you are doing documentation improvements for <a href="https://docs.asp.net">ASP.NET docs</a>, you can save time for hundreds of developers. You are not saving particular company's money, but you are saving our (developers) money and what's even more important, time that can be invested somewhere else.</p>
<p>Another great example of small incremental improvements is <a href="https://github.com/jdalton">John-David Dalton</a>. Creator of <a href="https://github.com/lodash/lodash">lodash</a>. He is contributing code on github every(!) day for a few years now. This is his github contributions chart:</p>
<p><img class="aligncenter size-full wp-image-17091" src="{{ site.baseurl }}/assets/2017/03/jdalton_github_contributions.png" alt="John-David Dalton contributions" width="742" height="200" /></p>
<p>No white squares. Some of his daily commits are <a href="https://github.com/lodash/lodash/commit/ba52c744aea55a385ea6604faf73245fa8b9bc85">tiny</a>, some are <a href="https://github.com/lodash/lodash/commit/9260bd2f57d619d3d3b56f1ecd1bc82766727b3e">small.</a> By being consistent every day, over years he was able to create <a href="https://www.sitepoint.com/top-javascript-frameworks-libraries-tools-use/">one of the most popular JavaScript library</a>.</p>
<p>What small improvement can you do in your project? Think about it, and remember that best ideas are born when you are away from your computer!</p>

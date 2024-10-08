---
layout: post
title: Trying iOS 11 with Xamarin
date: 2017-09-01 11:12:23.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- ios
- ios11
- VSforMac
- Xamarin
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
  dsq_thread_id: '6112855117'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/trying-ios-11-with-xamarin/"
---
<p>The triathlon season is over. I completed all three, planned races for this year:</p>
<ol>
<li>Ironman 70.3 Coeur d'Alene</li>
<li>SeaFair Sprint Triathlon (new PR!)</li>
<li>Lake Meridian Olympic Triathlon (new PR!)</li>
</ol>
<p>I also finished <a href="http://www.redmondcyclingclub.org/RAMROD/RAMROD_course_information.html">RAMROD</a> (epic Ride Around Mt Rainier in One Day) and <a href="http://redmondcyclingclub.org/rides/Coursed'Equipe.html">Course d'Equipe</a>. The last bike ride for this season is <a href="http://granfondowhistler.com/">Gran Fondo Whistler</a> in two weeks.</p>
<p>In the meantime...</p>
<h3>The Winter is coming!</h3>
<p>Apple is cooking for us iOS 11, and I decided to give it a shot! It actually works nice.</p>
<ol>
<li>Install latest Xcode beta from <a href="https://developer.apple.com/download/">here</a></li>
<li>Install latest <a href="https://dl.xamarin.com/MonoTouch/Mac/xamarin.ios-10.99.5.13.pkg">Xamarin.iOS</a> (all links are <a href="https://releases.xamarin.com/category/preview/">here</a>, hint: version is 10.99, not 11 yet)</li>
<li>Set VS for Mac to Xcode-beta (Preferences -&gt; Projects -&gt; SDK Locations -&gt; Apple -&gt; Location)</li>
</ol>
<p>If you did everything correct you should be able to see new iOS11 simulator:</p>
<p><img class="aligncenter size-full wp-image-18993" src="{{ site.baseurl }}/assets/2017/09/iOS11Simulator-e1503980619876.png" alt="iOS 11 simulator" width="350" height="718" /></p>
<p>I encountered one issue: when deploying to device I got following errors:</p>
<p><em>Error: unable to find utility "lipo", not a developer tool or in PATH</em><br />
<em>Error: Failed to create the a fat library</em></p>
<p>Solution was to run the following command:</p>
<p><code>sudo xcode-select --switch /Applications/Xcode-beta.app/Contents/Developer/</code></p>
<p><a href="https://forums.xamarin.com/discussion/31493/mtouchtask-error-mt5206-failed-to-create-the-a-fat-library-please-review-the-build-log-mt5206">Related Xamarin Forums thread</a>.</p>
<h3>Summary</h3>
<p>So far everything works pretty well. Occasionally when I run VS for Mac it doesn't detect simulators, but after restart they are back!</p>
<p>Have you tried iOS 11 yet?</p>

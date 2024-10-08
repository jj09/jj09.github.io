---
layout: post
title: UI Acceptance Testing Accessibility
date: 2016-09-26 16:19:28.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- accessibility
- testing
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
  dsq_thread_id: '5175931980'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/ui-acceptance-testing-accessibility/"
---
<p><img class="aligncenter size-full wp-image-15761" src="{{ site.baseurl }}/assets/2016/09/accessibility_keywords.png" alt="Accessibility keywords" width="800" height="435" /></p>
<p>In the previous post <a href="http://jj09.net/unit-testing-accessibility/">Unit Testing Accessibility</a> I showed how to run accessibility check on HTML node with <a href="http://www.deque.com/products/axe/">aXe</a>. This approach can be used to test components of your website.</p>
<p>You can take your accessibility testing to the next level by adding accessibility check for entire pages.</p>
<p>Do you remember <a href="http://martinfowler.com/bliki/TestPyramid.html">Martin Fowler's testing pyramid</a>?</p>
<p><img class="aligncenter size-full wp-image-15771" src="{{ site.baseurl }}/assets/2016/09/test-pyramid.png" alt="testign pyramid" width="619" height="341" /></p>
<p>While high-level UI tests can detect the same issues that unit tests can, usually UI tests are slower to run. Sometimes it takes 30 seconds to 1 minute to run 1 UI test, while unit test can be run in less than 100 milliseconds. Ideally you should have the most common scenario covered by UI test, and all possible customizations (on the component level) covered by unit tests. You can also add UI tests for some complex combinations of your components, and when you are fixing a bug in situation that unit test cannot cover encountered scenario. Because as you know, while fixing a bug, you should add unit test covering buggy scenario.</p>
<p>In general, unit tests and UI tests should be complementary. UI test should indicate an issue, while unit test should help you to find a source of the problem.</p>
<p>In accessibility testing, high-level checks are very useful in detecting accessibility issues caused by some "small change". Once you detect accessibility violation, you should:</p>
<ol>
<li>narrow it down to particular unit of your website</li>
<li>add unit test to cover broken scenario</li>
<li>make sure it fails</li>
<li>fix the issue (by writing code)</li>
<li>make sure that unit test pass</li>
<li>make sure that end to end UI tests pass</li>
</ol>
<p>Check out Marcy Sutton's article: <a href="http://www.deque.com/blog/accessibility-testing-axe-webdriverjs/">Accessibility Testing with aXe and WebdriverJS</a>. She created sample <a href="https://github.com/marcysutton/axe-webdriverjs-demo">github repo</a> that is demonstrating how to set everything up.</p>

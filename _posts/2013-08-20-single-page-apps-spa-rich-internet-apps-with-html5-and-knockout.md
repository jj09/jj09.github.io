---
layout: post
title: 'Single Page Apps (SPA): Rich Internet Apps with HTML5 and Knockout'
date: 2013-08-20 11:06:03.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- html5
- javascript
- knockoutjs
- Open Source
meta:
  _yoast_wpseo_linkdex: '71'
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _yoast_wpseo_focuskw: single page apps
  _yoast_wpseo_metadesc: Overview of Single Page Applications (SPA) and recommended
    tutorials.
  _syntaxhighlighter_encoded: '1'
  dsq_thread_id: '1655061896'
  _wp_old_slug: single-page-apps-spa-for-what-and-how-to
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/single-page-apps-spa-rich-internet-apps-with-html5-and-knockout/"
---
<blockquote>A rich Internet application (RIA) is a Web application that has many of the characteristics of desktop application software.</blockquote>
<p>We used to create Rich Internet Applications in Silverlight. Now, JavaScript frameworks (e.g. Knockout, Angular) are getting more popular for such purpose. Everything because of HTML5, which combined with them can easily provide nice development environment and rich experience.</p>
<p>However, all of those frameworks just take advantage of AJAX calls. So, what's big deal? </p>
<p>There is a few reasons. First one is the fact, that HTML5 <em>data-*</em> attribute allows to bind variables to HTML elements. We do not need to select them using id or class attributes. Another reason is variety of frameworks, which makes all of those AJAX calls behind the scenes. Additionally they do lot of other work such us serializing, models binding etc. They are just higher level of abstraction than jQuery.</p>
<h4>KnockoutJS</h4>
<p>One of the most popular JavaScript Framework is Knockout. It applies MVVM pattern. Its key features are:</p>
<ul>
<li>Declarative bindings (easily associate HTML elements with model)</li>
<li>Automatic UI Refresh (when data changes)</li>
<li>Dependency Tracking (chains of relationships)</li>
<li>Templating (easily generates UI depends on model data types) - e.g. we can use for loops in HTML</li>
</ul>
<p>KnockoutJS is open source framework, created by <a href="http://blog.stevensanderson.com/">Steve Sanderson</a>.</p>
<p>If you want to get started with SPA I recommend you <a href="http://knockoutjs.com/">knockoutjs.com</a> website and John Papa's series at Pluralsight.net: <a href="http://pluralsight.com/training/courses/TableOfContents?courseName=knockout-mvvm"> Building HTML5 and JavaScript Apps with MVVM and Knockout</a> and <a href="http://pluralsight.com/training/courses/TableOfContents?courseName=single-page-apps-jumpstart"> Single Page Apps JumpStart</a> (in this course John is taking advantage of various JS libraries to create consistent Single Page Appliation). </p>
<p>The biggest advantage of all JS libraries from my point of view is the possibility to do more (functionalities) with less (code). In other words: avoid rewriting boilerplate code.</p>
<p><b>EDIT:</b> You should also check John Papa's <a href="http://www.johnpapa.net/hottowel/">HotTowel</a> project template for Visual Studio, which gives you great start point for building SPA. It contains many JS libraries (e.g. Knockout and Durandal) for Rich Internet Apps development. More info on <a href="http://www.johnpapa.net/hottowel/">John's blog</a>. Thanks to nilphilus and Piotr Ptak for mentioning about it in comments.</p>

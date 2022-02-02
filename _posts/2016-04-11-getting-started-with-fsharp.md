---
layout: post
title: Getting started with F#
date: 2016-04-11 19:17:34.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- F#
- fsharp
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
  _oembed_94ad5360d09b8af584725d7a623bacd9: "{{unknown}}"
  builder_switch_frontend: '0'
  dsq_thread_id: '4739773328'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/getting-started-with-fsharp/"
---
<p><img class="aligncenter size-full wp-image-13581" src="{{ site.baseurl }}/assets/2016/04/fsharp-logo.png" alt="F#" width="256" height="256" /></p>
<p><strong>tl;dr This post is a list of resources for learning F# and overview of my mini-project: Stock Estimator.</strong></p>
<p>I couldn't resist anymore, and I finally tried F#. For the first two days it was painful. Some elements of F# syntax are weird. However after getting use to that, F# became a joy, and instead of a week (as I planned) I spent with F# almost two months.</p>
<h2>Getting Started</h2>
<ul>
<li><a href="https://app.pluralsight.com/library/courses/fsharp-jumpstart">F# Jumpstart (Pluralsight)</a> 1h 25m - brief introduction to F#, good for the beginning the get the sneak peak</li>
<li>Introduction to F# by <a href="https://twitter.com/dsyme">Don Syme</a> (<a href="https://channel9.msdn.com/Series/C9-Lectures-Dr-Don-Syme-Introduction-to-F-/C9-Lectures-Dr-Don-Syme-Introduction-to-F-1-of-3">part1</a>, <a href="https://channel9.msdn.com/shows/Going+Deep/C9-Lectures-Dr-Don-Syme-Introduction-to-F-2-of-3/">part2</a>, <a href="https://channel9.msdn.com/shows/Going+Deep/C9-Lectures-Dr-Don-Syme-Introduction-to-F-3-of-3/">part3</a>)</li>
<li><a href="http://dungpa.github.io/fsharp-cheatsheet/">F# Cheatsheet</a> - great overview of F# features</li>
<li><a href="https://vimeo.com/131640714">F# for C# Developers</a> by <a href="http://trelford.com/blog/">Phillip Trelford</a></li>
<li><a href="https://channel9.msdn.com/posts/Understanding-the-World-with-F">Understanding the World with F#</a> by <a href="http://tomasp.net/">Tomas Petricek</a></li>
<li><a href="http://www.tryfsharp.org/">Try F#</a> - interactive tutorial for learning F# (works only in IE because of Silverlight)</li>
<li><a href="https://github.com/ChrisMarinos/FSharpKoans">Functional Koans - F#</a> - collection of F# exercises inspired by <a href="http://github.com/edgecase/ruby_koans">Ruby koans</a> that requires you to fix failing unit tests one by one (fun and informative!)</li>
</ul>
<h2>Deep Dive</h2>
<ul>
<li><a href="https://sachabarbs.wordpress.com/1406-2/">F# for beginners</a> by Sacha Barber (Microsoft MVP) - extensive overview of almost all features of F# language (good as reference)</li>
<li><a href="https://app.pluralsight.com/library/courses/accessing-data-fsharp-type-providers">Accessing Data with F# Type Providers (Pluralsight)</a> by <a href="http://tomasp.net/">Tomas Petricek</a> (2h 14m)</li>
<li><a href="https://app.pluralsight.com/library/courses/fsharp-functional-data-structures">F# Functional Data Structures (Pluralsight)</a> (3h 44m) - deep dive into F# Data Structures</li>
<li><a href="https://app.pluralsight.com/library/courses/fsharp-type-driven-development">Type-Driven Development with F# (Pluralsight)</a> by <a href="http://blog.ploeh.dk/">Mark Seemann</a> (3h 56m)</li>
<li><a href="http://fsharpforfunandprofit.com/">F# for fun and profit</a> - solid source of knowledge to learn more about F# (when you know the basics)</li>
<li><a href="http://fsharp.org/">fsharp.org</a> - encyclopedia of resources for all topics related to F#</li>
<li>F# Advent Calendar <a href="http://sergeytihon.wordpress.com/2014/11/24/f-advent-calendar-in-english-2014/">2014</a> and <a href="https://sergeytihon.wordpress.com/2015/10/25/f-advent-calendar-in-english-2015/">2015</a> - set of articles about different topics related to F#</li>
<li><a href="https://vimeo.com/97507575">Domain modelling with the F# type system</a> by <a href="https://twitter.com/scottwlaschin">Scott Wlaschin</a></li>
<li><a href="https://vimeo.com/97344498">Railway Oriented Programming — error handling in functional languages</a> by <a href="https://twitter.com/scottwlaschin">Scott Wlaschin</a></li>
<li><a href="https://www.youtube.com/watch?v=MHvr71T_LZw">Domain-Driven Design, Event Sourcing and CQRS with F# and EventStore</a> by <a href="http://gorodinski.com/">Lev Gorodinski</a></li>
</ul>
<p>There is also a book written by Jon Skeet and Tomas Petricek: <a href="http://www.amazon.com/Real-World-Functional-Programming-With-Examples/dp/1933988924">Real World Functional Programming: With Examples in F# and C#</a>.</p>
<h2>Testing</h2>
<ul>
<li><a href="https://app.pluralsight.com/library/courses/fsharp-unit-testing">Unit Testing with F# (Pluralsight)</a> by <a href="http://blog.ploeh.dk/">Mark Seemann</a> (1h 32m)</li>
<li><a href="https://app.pluralsight.com/library/courses/fsharp-property-based-testing-introduction">Introduction to Property-based Testing with F# (Pluralsight)</a> by <a href="http://blog.ploeh.dk/">Mark Seemann</a> (1h 34m)</li>
<li><a href="https://app.pluralsight.com/library/courses/fsharp-test-driven-development">Test-Driven Development with F# (Pluralsight)</a> by <a href="http://blog.ploeh.dk/">Mark Seemann</a> (2h 17m)</li>
</ul>
<h2>Web Development</h2>
<p>The most popular F# Web Framework is <a href="https://github.com/SuaveIO/suave">Suave</a>. There is great <a href="https://www.gitbook.com/book/theimowski/suave-music-store/details">SuaveMusicStore tutorial</a> (<a href="https://github.com/theimowski/SuaveMusicStore">code</a>), which is inspired by <a href="http://www.asp.net/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1">ASP.NET MVC Music Store tutorial</a>. If you want to build Web API with F#, check <a href="http://blog.tamizhvendan.in/blog/2015/06/11/building-rest-api-in-fsharp-using-suave/">Building REST Api in Fsharp Using Suave</a>.</p>
<p>It is also worth to check <a href="https://vimeo.com/131641270">End-to-end Functional Web Development</a> by <a href="http://tomasp.net/">Tomas Petricek</a> where he showcases building web app with Suave.</p>
<p>For more, check <a href="http://fsharp.org/guides/web/">Web Programming with F# Guide</a>.</p>
<h2>Stock Estimator</h2>
<p>I created F# based app for predicting future stock prices ($1,000,000 idea!). The back-end is written in F#, and communicates with stock data API (Yahoo Finance) through F# type provider. There is also Suave Web API (microservice), and ASP.NET Core web app that communicates with it. Front-end is powered by <a href="http://aurelia.io/">Aurelia Framework</a>, and <a href="https://d3js.org/">D3 library</a>. In other words: I built F# microservice, consumed it from non-F# app, and have reusable logic in separated project. All communication with microservice happens through the client (with Aurelia Framework). So, there is no usage of F# from C#, but...I also created simple Console app (with C#) that uses mentioned F# logic. There is also Windows Forms app for displaying estimates, written in F#, that also use reusable logic.</p>
<p>Entire source code is available on <a href="https://github.com/jj09/StockEstimator">github</a>. Check it out!</p>
<h2>Summary</h2>
<p>Programming in F# is pure joy! It's a great language for working with data. Moreover, F# fits perfectly into today's World of microservices. You don't have to rewrite your already existing app, or create entire app with F#. You can just create one microservice with F#, and see how it works for you!</p>

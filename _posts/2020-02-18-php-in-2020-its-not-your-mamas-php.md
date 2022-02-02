---
layout: post
title: PHP in 2020 it's not your mama's PHP
date: 2020-02-18 22:59:24.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags: []
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
  dsq_thread_id: '7878026672'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/php-in-2020-its-not-your-mamas-php/"
---
<p>I decided to write this post, because before joining Facebook I thought that PHP is just old, limited language from 2 decades ago when server was responsible for simple form parsing, and generating HTML.</p>
<p>I actually learned web development using PHP in mid-2000s, when I was in middle school. I created my personal blog, and website about very popular back then game Deluxe Ski Jump. I actually still have the source code and recently put it on Azure at <a href="http://dsjonline.azurewebsites.net/">dsjonine.azurewebsites.net</a> - it is in polish, and there is no database:P Didn't bother to update character encoding from ISO-8859-2 to UTF. Why I used ISO-8859-2? Because my cousin told me to do so! It was real copy/paste programmer back then! Good times :D</p>
<p>Mark Zuckerberg wrote first version of Facebook around that time using PHP too. <a href="https://en.wikipedia.org/wiki/LAMP_(software_bundle)">LAMP</a> stack was the way to go for web development in 2000s.</p>
<p>A few days after joining facebook I realized that PHP now is full blown OO language. It has classes, interfaces, abstract classes, dependency injection, etc. It is much closer to C# or Java than to PHP that I used to write 15 years ago. At facebook we use <a href="https://hacklang.org/">Hack</a> (typed PHP). It's awesome. You have the best of two Worlds: type safety and no compilation! Just save, and refresh to see your changes. Yay! As pure PHP performance is not the best, <a href="https://dan.hersam.com/2015/02/25/go-vs-node-vs-php-vs-hhvm-and-wordpress-benchmarks/">HHVM performance is an improvement</a>.</p>
<p>In PHP, you can access pretty much every module in the codebase without explicitly referencing it. That's an extra productivity boost. Or hack:) Intellisense in editors like <a href="https://nuclide.io/">Nuclide</a> (Atom) or VSCode is pretty good as well. When you add Facebook engineering systems, where everything is so neatly setup to prioritize productivity, you are in heaven :) I know most of PHP devs do not have that luxury, but just sayin' ;)</p>
<p>If you want to learn more about modern PHP, check out these resources:</p>
<ul>
<li><a href="https://phptherightway.com/">PHP the right way</a></li>
<li><a href="https://www.amazon.com/Modern-PHP-Features-Good-Practices-ebook/dp/B00TKVLL26">Modern PHP book</a></li>
<li><a href="https://www.youtube.com/watch?v=wCZ5TJCBWMg">25 years of PHP (by the Creator of PHP)</a></li>
<li><a href="https://www.amazon.com/Hack-HHVM-Programming-Productivity-Breaking-ebook/dp/B014VH495E">Hack and HHVM book</a></li>
</ul>
<p>As of February 2020, PHP is 5th most popular language on StackOverflow (<a href="https://stackoverflow.com/tags">source</a>)! Just recently taken over by python.</p>
<p>In any means I am not recommending you to learn PHP if you don't have to. Choose <a href="https://www.rust-lang.org/">Rust</a> or <a href="https://golang.org/">Go</a> instead! Just wanted to let you know, that PHP changed A LOT! PHP in 2020 is not PHP from Web 1.0 times.</p>

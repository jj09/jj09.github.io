---
layout: post
title: Programming Contest Tips
date: 2014-06-05 13:04:17.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- events
- programming
tags:
- algorithms
- contest
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  feature_size: blank
  builder_switch_frontend: '0'
  dsq_thread_id: '2739353749'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/programming-contest-tips/"
---
<p><img class="size-large wp-image-2121 aligncenter" src="{{ site.baseurl }}/assets/2014/06/programming_contest-785x217.jpg" alt="programming contest" width="785" height="217" /></p>
<p>Recently I participated in a few Programming Contests: <a href="http://jj09.net/garmin-programming-competition-2014/">Garmin Programming Competition 2014</a>, <a href="http://acm.cis.ksu.edu/">ACM programming contest at my University</a> and <a href="https://code.google.com/codejam/">Google Code Jam 2014</a>. I also remember my first contest in algorithms <a href="http://kpi-open.org/home/2011/">KPI-Open 2011</a>, in Kiev, Ukraine. It was for teams up to 3 people. There was 16 problems to solve during 2 days. We solved one.</p>
<p>In some contests, there is no access to the Internet. It was the case during my first contest (<a href="http://kpi-open.org/home/2011/">KPI-Open 2011</a>). We were able to use Java, C++ or Pascal. First problem we faced was: "HOW TO READ INPUT FROM CONSOLE IN JAVA?". None of us remembered. Fortunately, we knew how to do it in C++. Thus we had to use C++ for the first day. We were more proficient in Java though and it slower our development. Before day two, we created check-sheet (we could bring as much printed papers as we wanted) with <a href="http://www.mkyong.com/java/how-to-read-input-from-console-java/">reading input in Java</a> and some other tricks, which you usually google for. It allowed us to solve one problem. By solving problem I mean, to deliver solution, which pass tests in required amount of time. We solved 7-8 problems (or even more?) during those two days, but only 1 got accepted. It gave us <a href="http://kpi-open.org/results/2011/">64 place (among 83 teams)</a>.</p>
<p>A few months after that, I participated in <a href="http://acm.cis.ksu.edu/">ACM programming contest at Kansas State University</a> with one friend of mine. There was a progress: 1 problem solved in 5 hours (1 day). It is better that 1 problem in 2 days :) Last year, I was 1-person team, and I got 3 problems solved (I was somewhere around 6-10 place). This year: I also solved 3 problems, but it gave me 3rd place.</p>
<p>Last year, I was also participating in Google Code Jam. In this contest you just need to deliver solution for given input. You download input file from website and you have some amount of time to upload solution (usually up to 10 minutes). Additionally, in most of problems there is small input set and large input set. The large set has more test cases and/or bigger numbers (e.g. int is not enough to solve it).</p>
<p>The most important thing during the Programming Contests is time. Time, in which you solve the problem.</p>
<p>My general tips (based on competitions I participated in) how to prepare for programming contests:</p>
<ul>
<li>Make preparation before. Do not just walk-in (especially if it is your first contest). Check <a href="http://mrmbdctg.freehostia.com/contest_Tipsforbeginner.html">Programming Contest Year Plan - Yes a year Plan to be a better Programmer</a>.</li>
<li>Take <a href="http://www.amazon.com/Introduction-Algorithms-Thomas-H-Cormen/dp/0262033844/">Introduction to Algorithms</a> book to the contest.</li>
<li>Create (and print if no internet access is allowed) template for standard program. 90% of problems has N test cases. You need to parse it, compute solution and print. My approach is to read all input first and serialize it to e.g. Case class. Then I am looping through all cases and printing output. I prepared a <a href="https://github.com/jj09/GoogleCodeJam/blob/master/Template.csx">template file</a>, which allows me to save time during the contest.</li>
<li>Find out what languages/technologies are allowed during the contest and practice with it before the contest. Programming in Eclipse is different than programming in Visual Studio! Especially debugging.</li>
<li>Find out how you need to provide solution (send source code or just solution?) and how to read/write input/output.</li>
<li>If possible, find problems from previous editions of particular contest and practice by solving them.</li>
<li>Don't be afraid to write bad code. You don't need to comply with the best practices. It doesn't matter, whether your code is not <a href="http://en.wikipedia.org/wiki/SOLID_(object-oriented_design)">SOLID</a>. Your code is not readable? Who cares? Don't waste time for refactoring. If you really feel bad with the code your have written - refactor it <span style="text-decoration: underline;">after the contest</span>. The only thing, which matters is, whether it solve the problem efficiently. Check solutions of the best competitors at <a href="https://code.google.com/codejam/contest/2437491/scoreboard#vf=1">Google Code Jam World Finals 2013</a>. Can I write better code? Sure I can. But nobody cares, because they (not me) were the best in last year contest.</li>
</ul>
<p>Solving algorithmic problems is only part of programmers' skills toolset. If somebody is not good at it, it does not mean he is a bad programmer. He may be good at something else (e.g. programming embedded devices for aircrafts or designing the rocket system). However, it is good to practice problems solving and writing code. It is like daily workout. The programmer who wrote 1000 programs will be always better than one who wrote only 10. You will definitely <a href="http://macgyverdev.blogspot.se/2014/04/become-better-programmer-with.html">become a better programmer with programming challenges</a>.</p>
<p>My code for ACM contests and Google Code Jam is available on github:</p>
<ul>
<li><a href="https://github.com/jj09/KSU-ACM-Programming-Contests">KSU-ACM-Programming-Contests</a></li>
<li><a href="https://github.com/jj09/GoogleCodeJam">GoogleCodeJam</a></li>
</ul>
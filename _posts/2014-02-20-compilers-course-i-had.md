---
layout: post
title: Compilers course I had
date: 2014-02-20 11:32:02.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
- studies
tags:
- compilers
- Eclipse
- git
- Java
- TDD
- unit tests
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  dsq_thread_id: '2294686073'
  _wp_old_slug: compilers-course-at-kansas-state-university
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/compilers-course-i-had/"
---
<p>In the last semester (Fall 2013) I had a pleasure to take course CIS706 - Translator Design (aka Compilers) with <a href="http://people.cis.ksu.edu/~robby/">Dr Robby</a> at Kansas State University. It was great experience! I think it is the best course I have ever taken.</p>
<p>The way how this course is designed is just amazing. During course about compilers you will also learn many other useful things:</p>
<ul>
<li>Java</li>
<li>Eclipse</li>
<li>Source Control (git)</li>
<li>Unit Testing (JUnit) and TDD</li>
<li>Reading legacy code</li>
<li>Java Byte Code</li>
</ul>
<p>How? You have to build the compiler for simple, Java based language called ExtendedStaticJava. You have 4 homeworks: parsing, building AST (Abstract Syntax Tree), type checking and byte code generation. For each of them you have 'legacy' code, which implements compiler for StaticJava. Your task is to extend it to handle ExtendedStaticJava syntax. For each homework you get around 100 Unit Tests. Your grade depends on number of passing tests. If all test are passing you get 100%. Implementation does not matter...but you might need to pay for workarounds later, because each homework is based on the code from previous one. I experienced this. I made a few hacks in first homework and then I needed to fix them during homework 2. It cost me extra time and I had to send incomplete solution. It is exactly how it goes in "Real World"! </p>
<p>For final project (last month of semester) we needed to create ExtendedStaticJava to C transpiler with Garbage Collector. Transpiler is source-to-source compiler. In other words: resulting code was C with Garbage Collector calls (GC was also implemented by us in C). We reused our homeworks (without byte code generation part) and generated C code (with GC calls) using <a href="http://www.stringtemplate.org/">StringTemplate</a>.</p>
<p>Let's take a look how all above help us to be better developers. </p>
<p>Most of students probably already know Java. If not - this course is the best time to learn. Java and C# are the most popular, static typing programming languages (today). When you learn one of them - it is easy to catch up with another. Java is still the most popular language in case of job offers (<a href="http://www.javacodegeeks.com/2013/02/traditional-programming-language-job-trends-2013-02.html">source</a>):</p>
<p><img src="{{ site.baseurl }}/assets/2014/02/traditionalLanguageJobTrends-Indeed.png" alt="traditional Language Job Trends - Indeed" width="540" height="300" class="aligncenter size-full wp-image-877" /></p>
<p>Thus, probability that you will be programming in Java after you graduate is pretty high. When you will be programming in Java, you will be probably using <a href="http://answers.yahoo.com/question/index?qid=20130220082953AACCzwM">Eclipse - its most popular IDE</a>. Another 'standard' in industry is Source Control. If the company you are working for is not using it - you should change your company(!), because something wrong is going on there. If you are not familiar with <a href="http://git-scm.com/">git</a> (leader in Open Source community, now being adapted by the industry) then this course is the best time to learn. Nowadays, even big companies (e.g. Microsoft) open sourcing their code (e.g. <a href="https://aspnet.codeplex.com/">ASP.NET</a> or <a href="https://github.com/SignalR/SignalR">SignalR</a>), which is available through git.</p>
<p>Unit testing is very popular nowadays. Lots of commercial projects use this technique to ensure software quality and development stability. Many projects are also using TDD (Test Driven Development) approach. First your write the test (as the requirement) and then code. When test pass, you refactor the code. During the course we were using JUnit (for now: No.1 Unit Test Framework for Java). Additionally, when you learn how to work with Unit Tests, then picking up a different framework is very easy (even in different language).</p>
<p>Software Development is a team work. Because of that, you will need to read code of other developers everyday. In most of courses during your University career you need to create some applications from scratch. Sometimes you are working in team of 2 or 3 people. Then in your first job, you get 100 000 lines of code written by somebody else. Often without documentation and sometimes people who wrote this code are not working there anymore. In other words - you're screwed. Compilers class will prepare you for that. During the course you will need to understand the existing code (StaticJava compiler), extend it and introduce some changes to get ExtendedStaticJava compiler working and Unit Tests passing.</p>
<p>Besides learning Java, you will also learn how JVM (Java Virtual Machine) and ByteCode are working. The idea of intermediate code is also used in C#: code is compiled to an Intermediate Language (IL) which then runs in the Common Language Runtime (CLR). It is very helpful for understanding how high-level code is translated to Assembly language.</p>
<p>It is also worth to mention about the essence of the course: compilers. The course is based on the popular <a href="http://www.amazon.com/Compilers-Principles-Techniques-Tools-Edition/dp/0321486811">Dragon Book</a>. You will learn about every stage of compiling: lexical analysis, parsing, creating AST (Abstract Syntax Tree), semantic analysis, optimization and code generation. For parsing and AST creation you will use <a href="http://www.antlr.org/">ANTLR</a>, which is the most popular tool for such purpose nowadays. Finally you will get understanding, what is going on between your high-level code and electrical impulses flowing in your computer.</p>
<p>Even if you know all of these things (Java, Eclipse, git, Unit testing) it is still worth to take this class. You will apply your knowledge in practice and learn about compilers. This knowledge is useful not only to understand how computers work, but also to learn about algorithms and data structures, which are applied there.</p>
<p>You can find more information about CIS706 on <a href="http://compilers.santoslab.org/">compilers website</a>. Moreover the StaticJava code is available on github: <a href="https://github.com/santoslab/compiler">github.com/santoslab/compiler</a>. There is also nice <a href="https://class.coursera.org/compilers-003">Compilers Course by Stanford University on Coursera</a>, which can be used as supplement for this class.</p>

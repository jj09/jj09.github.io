---
layout: post
title: Why you should read "The Pragmatic Programmer"
date: 2013-08-13 10:03:05.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- books
- programming
tags:
- book review
meta:
  _yoast_wpseo_linkdex: '67'
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _yoast_wpseo_focuskw: pragmatic programmer book review
  _yoast_wpseo_metadesc: The review of 'The Pragmatic Programmer' book by Andrew Hunt
    and Dave Thomas
  dsq_thread_id: '1603676796'
  feature_size: blank
  builder_switch_frontend: '0'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/why-you-should-read-the-pragmatic-programmer/"
---
<p><a href="http://amzn.to/2oN9m5H"><img class="alignright size-full wp-image-520" src="{{ site.baseurl }}/assets/2013/08/the_pragmatic_programmer.jpg" alt="The Pragmatic Programmer cover" width="300" height="382" /></a></p>
<p>Finally I read book written by Andrew Hunt and Dave Thomas: <a href="http://amzn.to/2oN9m5H">The Pragmatic Programmer</a>. It was published in 1999, but it is still valid. The main idea provided by this book is the way of thinking. In other words: how 'The Pragmatic Programmer' should behave and what actions he should take in various situations.</p>
<p>There are also tips which skills are useful for programmer (e.g. using perl/bash scripts, mastering command line and at least one text editor).</p>
<p>Some advices are not valid in any case. E.g. in my opinion tip to never leave broken functionality has exceptions. Especially when it is some minor bug. There are situations when it is better to first focus on most important features and the problematic one leave for the end. After all we will have a few minor bugs and working main functionality. Instead of solved some or even only one, hard minor bug (like css styling:)) and not implemented main functionalities.</p>
<p>The other well-known (or should be well-known) tips like use Source Control, learn new technologies, analyze mistakes from past projects are also mentioned and described.</p>
<p>Here you can find list of tips from the book in nutshell: <a href="http://pragprog.com/the-pragmatic-programmer/extracts/tips">http://pragprog.com/the-pragmatic-programmer/extracts/tips</a>. It is kind of summary of the book content.</p>
<p>At the and of each chapter, there is a set of exercises. This one blew my mind:</p>
<blockquote><p>A quick reality check. Which of these "impossible" things can happen?</p>
<ol>
<li>A month with fewer than 28 days.</li>
<li><em>stat("." ,&amp;sb) == -1</em> (that is, can't access the current directory)</li>
<li>In C++: <em>a=2;b=3; if (a+b!=5) exit(l);</em></li>
<li>A triangle with an interior angle sum != 180°</li>
<li>A minute that doesn't have 60 seconds</li>
<li>In Java: <em>(a + 1) &lt;= a</em></li>
</ol>
</blockquote>
<p>Fortunately at the end of the book there are answers (I wouldn't even start googling, due to 100% certainty that some of them just <b>can not</b> happen, like 1 or 5):</p>
<blockquote>
<ol>
<li>September, 1752 had only 19 days. This was done<br />
to synchronize calendars as part of the Gregorian<br />
Reformation.</li>
<li>The directory could have been removed by another<br />
process, you might not have permission to read it,<br />
&amp;sb might be invalid—you get the picture.</li>
<li>We sneakily didn't specify the types of a and b.<br />
Operator overloading might have defined +, =, or !<br />
= to have unexpected behavior. Also, a and b may<br />
be aliases for the same variable, so the second<br />
assignment will overwrite the value stored in the first.</li>
<li>In non-Euclidean geometry, the sum of the angles of<br />
a triangle will not add up to 180°. Think of a triangle<br />
mapped on the surface of a sphere.</li>
<li>Leap minutes may have 61 or 62 seconds.</li>
<li>Overflow may leave the result of a + 1 negative (this<br />
can also happen in C and C++).</li>
</ol>
</blockquote>
<p>Summarizing: <a href="http://amzn.to/2oN9m5H">The Pragmatic Programmer</a> contains huge amount of tips, which can help you to become better programmer. You may already know some of them (or most of them). In that case you will recall why they are important. Even Scott Hanselman said on his blog (in post <a href="http://www.hanselman.com/blog/SixEssentialLanguageAgnosticProgrammingBooks.aspx">Six Essential Language Agnostic Programming Books</a>), that he 'like to read this book at least every six months or so'.</p>
<p>It is 352 pages book. Can be easily read within 2 weeks by 1 hour reading per day. In my opinion it is one of must-read for programmer.</p>

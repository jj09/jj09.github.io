---
layout: post
title: Programming Pearls
date: 2014-12-08 20:54:20.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- books
tags:
- book review
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
  _syntaxhighlighter_encoded: '1'
  builder_switch_frontend: '0'
  dsq_thread_id: '3304887572'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/programming-pearls/"
---
<p><img class="aligncenter size-full wp-image-5831" src="{{ site.baseurl }}/assets/2014/12/programming-pearls-cover.jpg" alt="Programming Pearls" width="360" height="453" /></p>
<blockquote><p>Just as natural pearls grow from grains of sand that have irritated oysters, these programming pearls have grown from real problems that have irritated real programmers.</p></blockquote>
<p>I just finished reading Jon Bentley's book: <a href="http://www.cs.bell-labs.com/cm/cs/pearls/">Programming Pearls</a>. I read this book after <a href="http://www.hanselman.com/blog/SixEssentialLanguageAgnosticProgrammingBooks.aspx">Scott Hanselman's</a> and <a href="http://blog.codinghorror.com/recommended-reading-for-developers/">Jeff Atwood's</a> recommendations.</p>
<p>The problems analyzed in this book are still actual. However, I think that today programmers face slightly different challenges. Most of the problems described in this book are already solved in the libraries, or not often existing anymore (e.g., pretty printing on the console). I read the 2nd edition published in 1999, and most of problems require update to nowadays environments. For example: variable naming suggest the need to save the memory. E.g., <em>l</em>, <em>u</em>, <em>x</em>.</p>
<p>[c]int binarysearch1(DataType t)<br />
{	int l, u, m;<br />
	l = 0;<br />
	u = n-1;<br />
	for (;;) {<br />
		if (l &gt; u)<br />
			return -1;<br />
		m = (l + u) / 2;<br />
		if (x[m] &lt; t)<br />
			l = m+1;<br />
		else if (x[m] == t)<br />
			return m;<br />
		else /* x[m] &gt; t */<br />
			u = m-1;<br />
	}<br />
}[/c]</p>
<p>In the interview ("Epilog to second edition"), the author argues that programming style he used should not be used in large software projects. Let's take this excuse.</p>
<h3>Book overview</h3>
<p>Part I is a set of useful, general advises how to tackle programming problems. One caveat: nowadays we use unit testing instead of assertions and "scaffolding" (described in chapter 5). However, it might be useful in some environments with some particular circumstances.</p>
<p>Part II is about performance. Chapter 6 describe different optimization techniques. Although the tips are useful, today we are doing optimization on higher levels. I wonder if at least 1% of today programmers would be able to improve program performance, by rewriting assembly code. Anyway, this chapter shows that performance improvements can be done on different levels: algorithms, data structures, system architecture, underlying software, and even hardware. I like chapter 9, where author presents some very sophisticated tricks.</p>
<p>Part III (Columns 11-15) is about algorithms. Although it shows interesting analysis and fundamental algorithms (for sorting, and searching), I would rather recommend some solid algorithms book (e.g. <a href="http://www.amazon.com/Introduction-Algorithms-Thomas-H-Cormen/dp/0262033844">Introduction to Algorithms</a> by Cormen et al).</p>
<h3>Summary</h3>
<p>Programming Pearls shows which parts of software development changed, during last 15 years, but some parts of this book still remain valid. Moreover, this book is a good history lesson showing by example the advancement in software and hardware.</p>
<p>This book has many references to <a href="http://www.amazon.com/Code-Complete-Practical-Handbook-Construction/dp/0735619670">Steve McConnell's Code Complete</a>, and <a href="http://www.amazon.com/The-Mythical-Man-Month-Engineering-Anniversary/dp/0201835959">The Mythical Man-Month</a>. These books are on my to-read list for some time, and I will definitely read them in the near future.</p>
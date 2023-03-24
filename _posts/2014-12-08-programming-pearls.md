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
<p>I just finished reading Jon Bentley's book: <a href="https://amzn.to/404d6PL">Programming Pearls</a>. I read this book after <a href="http://www.hanselman.com/blog/SixEssentialLanguageAgnosticProgrammingBooks.aspx">Scott Hanselman's</a> and <a href="http://blog.codinghorror.com/recommended-reading-for-developers/">Jeff Atwood's</a> recommendations.</p>
<p>The problems analyzed in this book are still actual. However, I think that today programmers face slightly different challenges. Most of the problems described in this book are already solved in the libraries, or not often existing anymore (e.g., pretty printing on the console). I read the 2nd edition published in 1999, and most of the problems require updates to nowadays environments. For example: variable naming suggests the need to save memory. E.g., <em>l</em>, <em>u</em>, <em>x</em>.</p>
{% highlight c %}
int binarysearch1(DataType t)
{	int l, u, m;
	l = 0;
	u = n-1;
	for (;;) {
		if (l > u)
			return -1;
		m = (l + u) / 2;
		if (x[m] < t)
			l = m+1;
		else if (x[m] == t)
			return m;
		else /* x[m] > t */
			u = m-1;
	}
}
{% endhighlight %}

<p>In the interview ("Epilog to second edition"), the author argues that the programming style he used should not be used in large software projects. Let's take this excuse.</p>

<h3>Book overview</h3>
<p>Part I is a set of useful, general advice on how to tackle programming problems. One caveat: nowadays we use unit testing instead of assertions and "scaffolding" (described in chapter 5). However, it might be useful in some environments with some particular circumstances.</p>
<p>Part II is about performance. Chapter 6 describes different optimization techniques. Although the tips are useful, today we are doing optimization on higher levels. I wonder if at least 1% of today's programmers would be able to improve program performance, by rewriting assembly code. Anyway, this chapter shows that performance improvements can be done on different levels: algorithms, data structures, system architecture, underlying software, and even hardware. I like chapter 9, where the author presents some very sophisticated tricks.</p>
<p>Part III (Columns 11-15) is about algorithms. Although it shows interesting analysis and fundamental algorithms (for sorting and searching), I would rather recommend some solid algorithms book (e.g. <a href="https://amzn.to/3ZfvaVL">Introduction to Algorithms</a> by Cormen et al).</p>

<h3>Summary</h3>
<p><a href="https://amzn.to/404d6PL">Programming Pearls</a> shows which parts of software development changed, during the last 15 years, but some parts of this book remain valid. Moreover, this book is a good history lesson showing by example the advancement in software and hardware.</p>
<p>This book has many references to <a href="https://amzn.to/3TDBJ3c">Steve McConnell's Code Complete</a>, and <a href="https://amzn.to/40xPqTK">The Mythical Man-Month</a>. These books are on my to-read list for some time, and I will read them shortly.</p>

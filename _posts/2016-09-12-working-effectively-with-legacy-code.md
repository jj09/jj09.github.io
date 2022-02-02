---
layout: post
title: Working Effectively with Legacy Code
date: 2016-09-12 21:13:49.000000000 -07:00
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
- TDD
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
  dsq_thread_id: '5140048303'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/working-effectively-with-legacy-code/"
---
<p>I haven't publish any <a href="http://jj09.net/tag/book-review/">book review</a> for a while. It does not mean I am not reading books anymore. I just didn't feel that some of the books I <a href="https://www.goodreads.com/review/list/28888194-jakub?order=d&amp;shelf=read&amp;sort=date_read">read recently</a> requires my recommendation, or I didn't have any thoughts that I needed necessary to share right now.</p>
<p>I have added a few books to <a href="http://jj09.net/books/">my favorite books list</a> though. Check them out!</p>
<p>Working Effectively with Legacy Code deserves blog post because of a few reasons:</p>
<ol>
<li>Every Software Developer should read it</li>
<li>It's not really about legacy code</li>
<li>Published in 2004 (12 years ago!) is still very up to date</li>
</ol>
<p><img class="aligncenter size-full wp-image-15211" src="{{ site.baseurl }}/assets/2016/09/Working-Effectively-with-Legacy-Code-1st-Edition-by-Michael-Feathers-Michael-Feathers.jpg" alt="Working Effectively with Legacy Code 1st Edition by Michael Feathers (Michael Feathers)" width="500" height="663" /></p>
<p>The book has three parts:</p>
<ol>
<li>Importance of unit tests when changing software</li>
<li>Recipes for real World problems that we face when changing software (e.g., "I need to change a monster method" or "What methods should I test when introducing a change")</li>
<li>Dependency-breaking techniques catalog</li>
</ol>
<p>The first part should be familiar to most of programmers these days. If it is not for you then you should read <a href="http://jj09.net/agile-principles-patterns-and-practices-in-c-sharp/">Agile Principles, Patterns and Practices</a> (by <a href="http://cleancoder.com/">Robert Martin</a>), <a href="https://www.amazon.com/Test-Driven-Development-Kent-Beck/dp/0321146530">TDD by Example</a> (by <a href="https://en.wikipedia.org/wiki/Kent_Beck">Kent Beck</a>), and <a href="https://www.manning.com/books/the-art-of-unit-testing-second-edition">The Art of Unit Testing</a> (by <a href="http://osherove.com/">Roy Osherove</a>). You can thank me later.</p>
<p>The second part is the essence of the book. It shows, by example, how to add new feature, make a change to existing code, or fix a bug. Most books about software development, present examples on very simple, clean code that we never see in real World. This book, takes some messy piece of code and shows how to make it testable, how to get rid of too many side effects, and clean it up by separating dependencies and responsibilities. Many times we want to test one functionality, and then we realize that we need to instantiate tens of objects that other method depends on. Sounds familiar? This chapter shows how to handle that.</p>
<p>The last part (Dependency-Breaking Techniques) is very similar to <a href="http://www.martinfowler.com/">Martin Fowler's</a> <a href="https://www.amazon.com/Refactoring-Improving-Design-Existing-Code/dp/0201485672">Refactoring: Improving the Design of Existing Code</a>. It's a set of techniques, and step by step description how to apply them to existing code.</p>
<p>As I mentioned earlier. This book is not really about legacy code. I think it is more about evolving existing code. It is natural, when adding features, we add lines of code to the method. The hard part is to know when you should extract new method, or introduce a class, and refactor dependencies. It's OK to have global variables. The problem is to keep track of them or localize them. How do you know, that adding a new functionality will not break something? You have 100% test coverage for every possible use case? That's not possible because of complexity of software we are creating today. "What methods should I test" shows neat technique to backtrack effects, and side effects of a change that we are introducing.</p>
<p>There is much more, and you should check out this book. You don't have to read it from cover to cover. I strongly recommend you, at least, to scan through part 2 (changing software), and I am sure you will learn something new that you can apply for your project today!</p>

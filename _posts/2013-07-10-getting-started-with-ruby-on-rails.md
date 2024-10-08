---
layout: post
title: Getting started with Ruby on Rails
date: 2013-07-10 09:53:22.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- books
- programming
tags:
- ruby
- Ruby on Rails
- SublimeText
- tutorial
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _yoast_wpseo_metadesc: How to get started with Ruby on Rails. Tutorials, books and
    videos.
  dsq_thread_id: '1498548057'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/getting-started-with-ruby-on-rails/"
---
<p><img src="{{ site.baseurl }}/assets/2013/07/150px-Ruby_on_Rails.svg_.png" alt="Ruby on Rails logo" width="150" height="194" class="alignnone size-full wp-image-89" style="float: right" /></p>
<p>Recently I decided to learn Ruby on Rails. When you start learning a new technology you are always looking for the best available materials (to learn as efficient as possible). I did the same (using <a href="http://www.google.com">Google</a> and <a href="http://www.stackoverflow.com">StackOverflow</a>). Fortunately I found <a href="http://net.tutsplus.com/tutorials/ruby/the-best-way-to-learn-ruby-on-rails/">The Best Way to Learn Ruby on Rails</a> and I followed the recommended steps. With small modifications (extensions). </p>
<p>First of all I extended first step. Instead of just going through <a href="http://tryruby.org/">"Try Ruby"</a> exercises I also read first chapter of <a href="https://amzn.to/40uEshx">Seven Languages in Seven Weeks</a> (which is about Ruby). It was very good move, because this book is written in the way to show the flavors of language by comparison with others. I am a .NET guy, who was coding in PHP, C++, Java and Python before. Because of that I was more interested in the differences between Ruby and these languages, than in programming from ground up. I also reviewed (not read) <a href="http://www.humblelittlerubybook.com/">Humble Little Ruby Book</a>. It is a little bit more deep, but it gives you solid Ruby basics.</p>
<p>I was working with Rails on Windows and on Mac. Installing on Windows is very easy when you use <a href="http://railsinstaller.org/">RubyInstaller</a>. There is also version for Mac. However on Mac you can also install Rails using <a href="http://rvm.io/">RVM</a>. In that case I recommend you <a href="http://www.youtube.com/watch?v=MiAz0DnnY_k">installation screncast</a> by Michael Hartl.  On Windows I used <a href="http://railsinstaller.org/">RubyInstaller</a>, but on Mac I took advantage of Michael Hartl's screencast. Additionally you may also need <a href="http://sourceforge.net/projects/sqlitebrowser/">SQLite Database Browser</a> to browse your database easily. I did not know about it at the beginning and I was using <em>rails dbconsole</em>. Browsing with SQLite Database Browser is much more comfortable!</p>
<p>When I had Rails installed I went through <a href="http://net.tutsplus.com/tutorials/ruby/the-intro-to-rails-screencast-i-wish-i-had/">Jeffrey’s Introduction to Rails</a>. During that I tried to follow him, by writing code on my machine, but many times he was too fast. I needed to pausing video very often and even scrolling back to see written command (he was changing screens to quickly). Anyway it was very nice introduction and I recommend it. But you can skip rewriting and trying code he is writing. Just watch it to get a flavor of Rails.</p>
<p>After that I went through <a href="http://railsforzombies.org/">Rails for Zombies</a> tutorials. I was very lucky, because Code School had promotion in May 18-19, and they provided <a href="https://www.pluralsight.com/courses/code-school-rails-for-zombies">Rails for Zombies 2</a> for free in these days. These tutorials are very solid. The exercises force you to learn by typing, because you cannot proceed to next level, until you do not finish all tasks.</p>
<p><img src="{{ site.baseurl }}/assets/2013/07/AgileWebDevelopmentWithRails-243x300.jpg" alt="Agile Web Development with Rails cover" width="243" height="300" class="alignnone size-medium wp-image-92" style="float: right; margin: 10px" /></p>
<p>With all basics gained as described above I started a book: <a href="https://amzn.to/3LMzWa4">Agile Web Development with Rails</a>. I really like this book. It has 3 parts:</p>
<ul>
<li>Getting started (Rails installation, create first app, quick Rails architecture overview)</li>
<li>Building application (tutorial)</li>
<li>Rails in Depth</li>
</ul>
<p>The longest part of the book is the tutorial(2nd). Through this part you are creating an complete application exploring different Rails features. Unfortunately this book is a little bit outdated. Authors use ruby version 1.8.7 and Rails 3.0.0. I installed most recent versions: ruby 1.9.3p392 and Rails 3.2.13. Sometimes you need to fix the code (e.g. Chapter 11 - Task F: Add a Dash of Ajax). During that I found <a href="http://api.rubyonrails.org/">Ruby on Rails documentation</a> very useful. </p>
<p>The last part is going deep into Rails. I really recommend this part! It is not only about Rails, but also about Web Applications and MVC architecture in general: how browser works, how requests are handled by Rails app, session, cookies etc.</p>
<p>When I was in the middle of book I was a little bit angry (because it is outdated) and I switched to <a href="http://ruby.railstutorial.org/">Ruby on Rails tutorial</a> by Michael Hartl, which is strongly recommended on StackOverflow. Well...guys at SO are right. This is really good piece of knowledge not only about Rails, but also about using git, css, Bootstrap and Web Development in general. I really enjoyed it! If you do not want to buy videos, you can just read the <a href="http://ruby.railstutorial.org/ruby-on-rails-tutorial-book">free book</a> (it is the same content as in videos and more). There are also nice videos describing <a href="http://www.youtube.com/watch?v=FZ-b9oZpCZY">advanced setup</a> for Rails development on Mac and <a href="http://www.youtube.com/watch?v=05x1Jk4rT1A">SublimeText configuration for Rails</a>. Actually this tutorial covers Rails development from A to Z. </p>
<p>As a summary to the book and Michael Hartl's tutorial I reviewed <a href="http://guides.rubyonrails.org/">Rails Guides</a>. It is a nice overview for most important rails features. Can be also used as a reference. Some of the <a href="http://railscasts.com/">RailsCasts</a> are also useful.</p>
<p>I wanted to try a few different tutorials/books to see different approaches. E.g. Michael Hartl use rspec for unit tests, but the authors of Agile Web Development with Rails are using rails testing framework.</p>
<p>My adventure with Ruby (on Rails) lasts almost two months. Now I can admit that ROR is a very powerful and developer friendly framework. It contains many features, which are already grabbed by ASP.NET (e.g. migrations, bundling). What was surprising for me, you do not need IDE to develop Rails apps. I use <a href="http://www.sublimetext.com">SublimeText2</a> (awesome editor!) and it is really enough. Some Rails developers use VIM or Emacs. Of course there are some IDEs such as <a href="http://www.jetbrains.com/ruby/">RubyMine</a> or <a href="http://www.aptana.com/products/radrails">Aptana Studio</a>. I tried both. RubyMine seems to be pretty cool...but I stick with SublimeText. Additionally, during Rails development you spend lot of time with console (to create/run/undo migrations, create models/controllers, run tests etc.). </p>
<p>If you want to start Rails development, my recommended steps are:</p>
<ul>
<li>Read first chapter of <a href="https://amzn.to/40uEshx">Seven Languages in Seven Weeks</a> (it's about Ruby)</li>
<li>Watch <a href="http://net.tutsplus.com/tutorials/ruby/the-intro-to-rails-screencast-i-wish-i-had/">Jeffrey’s Introduction to Rails</a> (just watch it, without trying to follow him on your machine!)</li>
<li>Go through <a href="http://railsforzombies.org/">Rails for Zombies</a> tutorial</li>
<li>Install Rails: on Windows (<a href="http://railsinstaller.org/">RubyInstaller</a>) or on Mac (<a href="http://youtu.be/MiAz0DnnY_k">Michael's Hartl installation guide</a>)</li>
<li>Do <a href="http://ruby.railstutorial.org/">Ruby on Rails tutorial</a> by Michael Hartl</li>
<li>Read 3rd chapter of <a href="https://amzn.to/3LOIEES">Agile Web Development with Rails</a> (you can also read 1st and 2nd chapters, but its content is more or less covered by Michael Hartl's tutorial)</li>
<li>Create blog or some "your idea Rails app"</li>
</ul>
<p>You might also find these tools/resources useful:</p>
<ul>
<li><a href="http://api.rubyonrails.org/">Ruby on Rails documentation</a></li>
<li><a href="http://sourceforge.net/projects/sqlitebrowser/">SQLite Browser</a></li>
<li><a href="http://guides.rubyonrails.org/">Rails Guides</a></li>
<li><a href="http://railscasts.com/">RailsCasts</a></li>
</ul>
<p>What I like in Ruby on Rails? The syntax, convention over configuration and lots of implemented features in the framework layer. Moreover: Rails are just cool.</p>

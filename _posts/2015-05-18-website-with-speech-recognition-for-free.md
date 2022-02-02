---
layout: post
title: Website with speech recognition for free
date: 2015-05-18 20:48:52.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- voice recognition
- Web Speech API
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
  dsq_thread_id: '3775655812'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/website-with-speech-recognition-for-free/"
---
<p>A few weeks ago I blogged about <a href="http://jj09.net/voicecmdr-voice-commands-in-the-browser/">voiceCmdr</a> - library for adding voice commands to website (built on top of <a href="https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html">Web Speech API</a>).</p>
<p>I put up simple website - <a href="https://github.com/jj09/BooksLib">BooksLib </a>- a books library that allows up voting books, adding to favorites, and searching.</p>
<p>This application enables also voice interaction. You can check it live <a href="http://bookslib.azurewebsites.net/">here</a> (Azure) or <a href="http://books-lib.herokuapp.com">here</a> (Heroku).</p>
<p>It works in two modes:</p>
<ol>
<li>continuous - website is listening for commands continuously</li>
<li>single - website is listening for a single command, and stops listening after receiving</li>
</ol>
<p>You can enable one of two modes through panel on the top-right corner:</p>
<p><img class="aligncenter size-full wp-image-9721" src="{{ site.baseurl }}/assets/2015/05/bookslib-voicePanel.jpg" alt="BooksLib - voice panel" width="257" height="110" /></p>
<p>Available commands:</p>
<ul>
<li><em>Home</em> - go to home site</li>
<li><em>Books</em> - go to books site</li>
<li><em>Favorites</em> - go to favorites site</li>
<li><em>Top 10</em> - go to top 10 site</li>
<li><em>Search [phrase]</em> - search for given phrase (e.g. "Search JavaScript" will display all books with "JavaScript" phrase in title)</li>
<li><em>Favorite</em> - add currently displayed book to favorites (can be used only when single books is displayed)</li>
</ul>
<p>You can check how these commands were added in lines 60-85, in <a href="https://github.com/jj09/BooksLib/blob/master/public/app/app.js">app.js</a> file (only 25 lines including empty lines and brackets!).</p>
<p>To add voice commands to your website easily check out <a href="https://github.com/jj09/voiceCmdr">voiceCmdr</a> library.</p>
<p>* Voice commands works only in Google Chrome - the only web browser that <a href="https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API#Browser_compatibility">supports Web Speech API</a> so far.</p>

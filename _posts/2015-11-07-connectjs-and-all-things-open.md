---
layout: post
title: ConnectJS and All Things Open
date: 2015-11-07 15:54:43.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- events
- speaking
tags:
- AngularJS
- javascript
- node
- TypeScript
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
  dsq_thread_id: '4299120396'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/connectjs-and-all-things-open/"
---
<p>Last month I had a pleasure to speak at <a href="http://connect-js.com/">ConnectJS</a> and <a href="http://allthingsopen.org/">All Things Open</a> conferences.</p>
<h3>ConnectJS</h3>
<p><img class="aligncenter size-full wp-image-11741" src="{{ site.baseurl }}/assets/2015/11/connectjs2015.jpg" alt="ConnectJS 2015" width="800" height="279" /></p>
<p><a href="http://connect-js.com/">ConnectJS</a> was not only about JavaScript, but about web development in general. There was even track dedicated for UI Design and User eXperience. The most popular during the conference were talks about ES6/ES2015 and React.</p>
<p>I delivered two sessions:</p>
<p><strong>TDD with TypeScript, AngularJS and Node.js</strong></p>
<p>// video coming soon</p>
<p><a href="https://github.com/jj09/tdd-with-typescript-angularjs-nodejs">Code</a></p>
<p><strong>Aurelia - the next generation Framework you will love</strong></p>
<p>// video coming soon</p>
<p><a href="https://github.com/jj09/aurelia-demo">Code</a></p>
<p>I addition to my talks I attended the following sessions:</p>
<p><strong>Everything I Needed to Know, I Learned in Rabbinical School</strong> (Yitzchok Willroth) - this session was about sharing knowledge, and cooperation between developers. One thing I noticed, not only at conferences, but also at local meetups in Seattle area is that many people would like to go and speak at the conferences, but "they aren't doing anything interesting in day-to-day job and they are not expert in anything". They should have been at this session. Yitzchok was explaining how you can help others, and engage in Open Source. Moreover, he emphasized one, simple truth: every developer has something interesting to share.</p>
<p><strong><a href="http://blogs.msdn.com/b/dorischen/archive/2015/10/23/building-web-sites-that-work-everywhere.aspx">Building Web Sites that Work Everywhere</a></strong> (Doris Chen) - very useful overview of web compatibility problems, and recommendation of tools that can help with that, like <a href="http://autoprefixer.github.io/">Autoprefixer</a>. I also liked the quote from Patrick Lauke: "The userAgent property is ever-growing pack of lies". Doris recommended that we should prefer feature detection over relying on userAgent strings.</p>
<p><strong>Re-evaluating Front-end Performance Best Practices</strong> (Ben Vinegar) - the most important lesson learned at this session is the fact that whatever you find in JavaScript books written 2+ years ago might be already obsolete. Moreover, whatever you learn today, might be obsolete tomorrow. This is definitely not a good news for developers, but we need to deal with that and when reading anything on the web - thinking for ourselves.</p>
<p><strong>Video killed the Telephone Star</strong> (Ben Klang) - WebRTC is coming to the browser. In this talk Ben demonstrated web app that allows to do a video conference (his implementation of Google Hangouts in Rails).</p>
<p><strong>Lessons learned with TypeScript and ES2015</strong> (Dylan Schiemann) - it was an overview of TypeScript and ES6 based on experience working on <a href="https://dojotoolkit.org/community/roadmap/">Dojo 2 Framework</a> - the second largest application written in TypeScript (after Azure Portal). After this presentation I talked to Dylan, and he showed me another projects his company <a href="https://www.sitepen.com/">SitePen</a> is working on: <a href="https://theintern.github.io/">Intern</a> - very flexible and powerful testing framework, and <a href="https://sitepen.github.io/mayhem/guide/">Mayhem</a> - JS Framework written in TypeScript (still under development).</p>
<p><strong>Functional Programming Basics in ES6</strong> (Jeremy Fairbank) - tips&amp;tricks you can do in JavaScript(ES6), but you cannot in OO strongly typed languages like C# or Java.</p>
<p><strong>Lessons from Open Source @ Scale</strong> (Christine Abernathy) - Facebook has over 300 repos in github (after this talk I checked how many Microsoft have - almost 300). Christine explained how they help community by delivering Open Source, and how community helps them by contributing to their software.</p>
<p><strong>Introducing Trix</strong> (Javan Makhmali, Sam Stephenson) - Javan and Sam created web based text editor, and they <a href="https://github.com/basecamp/trix">open sourced it</a> right after this talk.</p>
<p><strong>The rise of "API" first applications</strong> (Travis Tidwell) - this talk was about Micro Services, and modern applications architecture where we have multiple, independent endpoints responsible for one functionality each.</p>
<p><strong>It Was Like That When I Got Here</strong> (Paul M. Jones) - it was a great talk about approaching legacy applications, and refactoring techniques. I enjoyed it even despite the fact that Paul was using PHP examples...I actually felt a bit sentimental as PHP was a language that get me started with Web Development when I was back in middle/high school :)</p>
<h3>All Things Open</h3>
<p><img class="aligncenter size-full wp-image-11761" src="{{ site.baseurl }}/assets/2015/11/allthingsopen2015.jpg" alt="All Things Open 2015" width="800" height="265" /></p>
<p><a href="http://allthingsopen.org/">All Things Open</a> is one of the largest Open Source conferences in the United States. This year there was over 1700 attendees, and 13 tracks!</p>
<p>I gave a talk about TDD with TypeScript, AngularJS, and Node.js - the same as at ConnectJS.</p>
<p><iframe width="854" height="480" src="https://www.youtube.com/embed/U_jAuqjn1B0" frameborder="0" allowfullscreen></iframe></p>
<p>On a day before the conference there was 5k run/sightseeing event at the evening. It was exactly what I needed before 2 days of seating. Kudos for organizers :)</p>
<p>Most of my time during the conference I spent in the room with front-end related sessions. Carina C. Zona explained problems with artificial intelligence and machine learning - Consequences of an Insightful Algorithm. Seth Vargo made an overview of Vargant - product that allows to create and configure universal development environment for every developer in the team. Christian Heilmann was encouraging people to learn JavaScript, ECMAScript 6, and to stop supporting old browsers, such as IE8, that has security vulnerabilities. Yehuda Katz explained how he and other contributors of Ember.js created version 2 without breaking a lot of APIs from version 1, and thus allowing developers for a smooth transition. I also liked the session about Netflix architecture by Andrew Spyker. I wish Andrew had more time to explain details more deeply. The surprising takeaway is that Netflix has 3x of everything. Which means - for every server, service and API they have additional 2 redundant.</p>
<p>The most widely commented session at the conference was <a href="http://www.zdnet.com/article/mark-russinovich-the-microsoft-azure-cloud-and-open-source/">keynote by Mark Russinovich</a>. I was pretty surprised that people were surprised by Microsoft doing so much Open Source. For me this is a known fact for a few years now, but it seems that the rest of the World doesn't know yet, and still see Microsoft as closed-source corporation that want to lock you in their technology.Well...that's not true anymore. I also had a pleasure to met <a href="https://www.christianheilmann.com">Christian Heilmann</a> - former Evangelist of Mozilla who joined Microsoft with one mission: kill the Internet Explorer. I really enjoyed his <a href="https://www.christianheilmann.com/2015/10/20/all-things-open-talk-the-es6-conundrum-slidesscreencastlinks/">session on ES6</a>, and keynote.</p>
<p>At the speaker dinner I had a pleasure to seat at the table with Andrew Spyker from Netflix, Michael Laing of New York Times, Christine Abernathy from Facebook, and Eric Martindale - entrepreneur from Silicon Valley. We had interesting conversation of the future of Netflix, Internet Television, bitcoin, and digital newspapers. I also learned that New York Times is the only news paper that is profitable in the transition from paper to electronic.</p>
<p>At All Things Open I finally got awesome Ninja Cat stickers:</p>
<p><img class="aligncenter size-full wp-image-11871" src="{{ site.baseurl }}/assets/2015/11/thinkpadx1-stickers.jpg" alt="ThinkPad X1 stickers" width="800" height="536" /></p>

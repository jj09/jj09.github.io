---
layout: post
title: 'dotNetConfPL 2014: summary and sessions recap'
date: 2014-10-26 20:08:35.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- events
tags:
- dotNetConfPL
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
  _wp_old_slug: dotnetconfpl-2014-summary-and-sessions-outlines
  dsq_thread_id: '3160076236'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/dotnetconfpl-2014-summary-and-sessions-recap/"
---
<p>The second edition of <a href="http://www.dotnetconf.pl">dotNetConfPL</a> was pretty successful. I am very pleased with all sessions, and speakers performance.</p>
<p>All sessions went smooth, but one. Barbara Fusinska could not run screenshare on Google Hangouts. Her session was recorded later and is <a href="http://dotnetconf.pl/Agenda">already available</a>. The only way to inform other about the problems during the conference was through JabbR or displaying Blue Screen of Death instead of her session. Adding something on website would require us to redeploy. We didn't want to do that. For the next year we will prepare some placeholder for information, which can be set dynamically.</p>
<p>This year we had one non-technical talk: <a href="https://www.youtube.com/watch?v=hbxTiQjtyt0">Talent for $2. You would be tempted to!</a> I think this talk has great potential. It includes a lot of pointers and tips. I encourage you to look at it. I watched <a href="http://www.ted.com/talks/simon_sinek_how_great_leaders_inspire_action">Simon Sinek's TED talk: "How great leaders inspire action"</a>, and I took <a href="https://www.gallupstrengthscenter.com/">Clifton's test</a> to discover my talents. My 5 talents are:</p>
<ul>
<li>Learner</li>
<li>Focus</li>
<li>Responsibility</li>
<li>Deliberative</li>
<li>Analytical</li>
</ul>
<p>I am very interested if some of you did this test, and what results did you get. Share it in comments!</p>
<p>The most popular feedback about the conference is: "We need it more often than once a year". We will try to figure out something ;)</p>
<p>Check all sessions recap:</p>
<h4>Maciej Aniserowicz - Unit testing in practice, vol 2</h4>
<p><iframe width="640" height="360" src="http://www.youtube.com/embed/zfyUQKktc4w" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>1:11 - agenda<br />
1:55 - unit tests vs integration tests<br />
4:14 - DB testing: "in memory"<br />
7:14 - DB create script<br />
7:50 - DEMO start<br />
9:25 - tests outline<br />
11:40 - creating <em>InMemoryDbFixture</em> (helper class for tests)<br />
13:40 - tests implementation<br />
17:00 - first method implementation (to pass test)<br />
18:29 - installing packages: <em>autofixture</em>, <em>xunit.extensions</em>, <em>autofixture.xunit</em> (for random string generation)<br />
19:30 - applying installed packages for automatic string generation<br />
21:15 - second method implementation (to pass test)<br />
24:20 - modifying <em>InMemoryDbFixture</em> class to respect join on tables<br />
26:12 - pros and cons for testing with real DB<br />
27:50 - separating tests for mock DB, and real DB<br />
30:09 - script for drop everything in DB<br />
32:15 - creating fixture for running db scripts (drop_everything.sql and install.sql)<br />
34:50 - baking fixture into test class and implementing tests for real DB<br />
42:00 - turning off NCrunch ability to run tests simultaneously<br />
43:40 - summary<br />
45:10 - Q&amp;A</p>
<h4>Filip Wojcieszyn - Everything you want to know about Roslyn</h4>
<p><iframe width="640" height="360" src="http://www.youtube.com/embed/akFWDp1v-Oo" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>1:55 - C# compiler today<br />
3:20 - compiler as a service<br />
4:05 - Roslyn influence<br />
6:45 - Roslyn APIs<br />
7:58 - Tools required for Roslyn<br />
10:25 - compiler as a service DEMO<br />
17:17 - Roslyn for code analysis (static, semantic)<br />
22:24 - code analysis with Roslyn DEMO (syntax visualizer)<br />
26:21 - sanity check DEMO<br />
31:40 - SyntaxRewriter DEMO<br />
35:55 - Roslyn APIs (one more time)<br />
38:40 - building tools for Visual Studio with Roslyn SDK<br />
39:25 - Diagnostic + Code fix DEMO<br />
46:57 - Custom C# dialect DEMO<br />
50:30 - Examples of Roslyn in Real World<br />
52:00 - Q&amp;A</p>
<h4>Barbara Fusinska - Aspect-Oriented Programming (AOP)</h4>
<p><iframe width="640" height="360" src="http://www.youtube.com/embed/es_qdXKSh7M" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>1:37 - Agenda<br />
3:29 - History of AOP<br />
4:57 - Cross cutting concerns<br />
8:50 - What the heck are aspects?<br />
13:01 - demo app presentation<br />
15:23 - Some benefits of AOP<br />
16:15 - DEMO: adding functionality to existing method of demo app<br />
23:55 - DEMO: LoggingAspect<br />
27:00 - DEMO: DefensiveProgrammingAspect<br />
28:23 - DEMO: TransactionAspect<br />
30:00 - Where you've been using AOP without knowing it<br />
33:15 - DEMO: communication with external services and cleaning code with aspects<br />
42:02 - Testing aspects usage<br />
46:10 - DEMO: How to test aspects and possible problems</p>
<h4>Jakub Gutkowski - Server Side or/and Client Side MVC ???</h4>
<p><iframe width="640" height="360" src="http://www.youtube.com/embed/SB994BIfW3k" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>0:45 - Agenda<br />
1:06 - Client Side vs Server Side<br />
6:22 - SPA (Single Page Applications)<br />
14:00 - Problems with SPA<br />
16:58 - Solutions?<br />
19:20 - DEMO: SPA inside not SPA<br />
23:39 - DEMO: SPA without server<br />
26:20 - JavaScript everywhere? JS approach by Twitter, Basecamp, AirBnB, Instagram, Facebook<br />
34:20 - How we can/should use JavaScript<br />
35:13 - DEMO: Push State<br />
40:53 - summary<br />
41:22 - Q&amp;A</p>
<h4>Patryk Góralowski - Talent for $2. You would be tempted to!</h4>
<p><iframe width="640" height="360" src="http://www.youtube.com/embed/hbxTiQjtyt0" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>3:39 - how to answer a question: who you are?<br />
6:05 - development<br />
6:59 - self development<br />
7:58 - our personal resources: body, mind, emotions, belifies<br />
14:00 - task 1: why your are here today? give 10 reasons, select 3 most important, and ask why each of them<br />
19:30 - expected result from task 1<br />
21:02 - about Simon Sinek (author of the process given in task 1) and his TED talk: <a href="http://www.ted.com/talks/simon_sinek_how_great_leaders_inspire_action">How great leaders inspire action</a><br />
26:35 - philosophy of our self development<br />
27:35 - about Mike Markkula, and philosophy of Apple<br />
29:34 - #1: empathy (understand customer needs better than others)<br />
30:32 - task 2: write down your needs<br />
30:53 - #2: focus (eliminate all irrelevances)<br />
31:29 - task 3: eliminate all irrelevances at your work<br />
33:10 - #3: impute desired characteristics<br />
35:55 - task 4: identify your "imputed characteristics"<br />
37:27 - invest $2 to discover your talent ($9.99 for 5 talents) with <a href="https://www.gallupstrengthscenter.com/">Gallup Strengths Center</a><br />
39:55 - what means talent by Gallup Institute<br />
42:06 - strength = talent + knowledge + skills<br />
43:33 - <a href="https://www.gallupstrengthscenter.com/">Clifton's test</a><br />
45:05 - 5 talents discovered by Patryk<br />
49:22 - summary<br />
50:46 - recommended books<br />
51:45 - Q&amp;A</p>
<h4>Maciej Grabek - Business Requirements in the form of a code: a few words about BDD with SpecFlow</h4>
<p><iframe width="640" height="360" src="http://www.youtube.com/embed/-OLJ0epfZ7U" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>1:25 - Agenda<br />
2:20 - DEMO #0: unit tests - how we do that, and challenges in interaction with business people<br />
5:03 - business requirements and unit tests (BDD)<br />
7:02 - Applying BDD (tools)<br />
9:25 - DEMO #1: simple example (translating behavior description to C# code)<br />
16:53 - DEMO #2: parameters<br />
18:45 - DEMO #3: scopes<br />
23:05 - DEMO #4: parameters table<br />
35:45 - DEMO #5: "before" and "after"<br />
42:19 - summary<br />
46:36 - Q&A</p>
<h4>Michał Łusiak - WTF # - what is F # and why you should care</h4>
<p><iframe width="640" height="360" src="http://www.youtube.com/embed/a-ce4aGZ18I" frameborder="0" allowfullscreen=""></iframe></p>
<p>0:41 - Functional programming<br />
4:38 - F# language overview<br />
10:41 - DEMO: variables<br />
14:07 - DEMO: lists<br />
15:59 - DEMO: functions<br />
19:53 - DEMO: pattern matching<br />
21:23 - DEMO: tuples<br />
22:20 - DEMO: record types<br />
23:04 - DEMO: union types<br />
24:01 - DEMO: printing<br />
25:00 - DEMO: using .NET libraries from F#<br />
25:55 - DEMO: unit of measures ("numbers with units" variables)<br />
28:21 - DEMO: type provides (providing types for compiler dynamically)<br />
31:12 - Why use F#<br />
33:18 - Learning resources<br />
38:05 - Recommended F# talks<br />
39:20 - Recommended books<br />
39:58 - summary<br />
40:10 - Q&A</p>

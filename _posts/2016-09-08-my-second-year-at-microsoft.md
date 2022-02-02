---
layout: post
title: My second year at Microsoft
date: 2016-09-08 11:54:22.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- career
- programming
tags:
- Microsoft
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
  _oembed_ffd11120a221b8ffcd6cc3512f970bb4: "{{unknown}}"
  _oembed_08b58f7ab6e141a9f6f7bb56721e3610: "{{unknown}}"
  _oembed_f6eb6d59358d11c93522040f91b0183d: "{{unknown}}"
  builder_switch_frontend: '0'
  dsq_thread_id: '5129594708'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/my-second-year-at-microsoft/"
---
<p><img class="aligncenter size-full wp-image-15451" src="{{ site.baseurl }}/assets/2016/09/Microsoft-badge.jpg" alt="Jakub Jedryszek - Microsoft badge" width="800" height="600" /></p>
<p>It feels like it was yesterday when I published <a href="http://jj09.net/my-first-year-at-microsoft/">My first year at Microsoft</a>. Time is going fast! This is what usually happen when you have a lot of things to do, and you enjoy it. My second year spent at Microsoft has been great! Full of new experiences, challenges, and lessons learned.</p>
<h3>Azure Portal</h3>
<p><img class="aligncenter size-full wp-image-14641" src="{{ site.baseurl }}/assets/2016/09/azure-portal-2016.png" alt="Azure Portal in 2016" width="800" height="444" /></p>
<p>For the past 2 years I've been working on the Azure Portal. Last 12 months has been very important for entire Portal team. Since December 2, 2015 the <a href="http://portal.azure.com">new Azure Portal</a> is no longer in preview, and is now <a href="https://azure.microsoft.com/en-us/blog/announcing-azure-portal-general-availability/">an official management interface for Azure</a>. <a href="http://manage.windowsazure.com">The Old Portal</a> is still available, but we slowly retire its features, and move them one by one to the new Portal. More, and more people start liking the new, revolutionary UI. We are getting requests to Open Source our UI, so that people can use it to build their own management interfaces. If you are interested in that, <a href="https://feedback.azure.com/forums/223579-azure-portal/suggestions/5048221-open-source-the-portal-blade-tech">vote here</a>.</p>
<p>Over last year I helped to improve Portal reliability, which was our last milestone before becoming the official management portal for Azure. It was one of the hardest things I've ever worked on, because of the <a href="http://jj09.net/azure-portal-the-largest-single-page-app-in-the-world/">Portal Architecture</a>. We started from 80% reliability in some areas, and our goal was to achieve 99.9%. It was extensive few months of investigation, bug fixing, and optimization. Once we achieved three nines, now we have to stay there. We are getting regressions from time to time, but for most of the time we keep the reliability at the desired level.</p>
<p>Another big area was improving <a href="http://jj09.net/web-accessibility-hacker-way/">accessibility (keyboard + screen reader support)</a>. It was very challenging task because, again, the Azure Portal is nothing like most of web apps. Especially from the design perspective. It's totally different, non-standard, and has a bunch of features nobody have done before (blades, tiles and journeys). As of today I am amazed how much progress have been done, and what the current state of Portal accessibility is. One thing that amaze me at Microsoft is how the smallest, tiniest, everyday improvements makes a difference in a long run.</p>
<p>Besides reliability and accessibility, I work mostly, on the web controls that are being exposed by our Framework. Partner teams (e.g., Web Apps, Virtual Machines, SQL, etc.) are building Azure features using our Framework and controls. Over last 12 months I created a few controls, added a lot of features to existing ones, fixed a tons of bugs, and made a lot of improvements for date/time controls with help from <a href="http://codeofmatt.com/">Matt Johnson</a> (yes, he does not work for our team, but he is one of the best date/time and timezone experts in the World, and it happened that he works for Microsoft so it would be stupid to not ask for his expert advice).</p>
<p>There is also one thing I need to rant about: <a href="http://caniuse.com/#search=intl">Safari 9.x (and all earlier versions) does not support Internationalization API (Intl)</a>. We are using Intl API for numbers and currency formatting. At the beginning, when we were still in preview, we hoped that Safari will add Intl support soon (in a year or so), but it didn't happen. We had to use <a href="https://github.com/andyearnshaw/Intl.js/">polyfill</a>. Oh...actually I should rant about other issues we had with Safari (like <a href="https://wouterdeschuyter.be/blog/local-storage-is-not-supported-with-safari-in-private-mode-1274581356">Local Storage does not work in private mode</a>), but you can check <a href="http://caniuse.com">caniuse.com</a> or just read an article: <a href="https://wouterdeschuyter.be/blog/local-storage-is-not-supported-with-safari-in-private-mode-1274581356">Safari is the new IE</a>.</p>
<p>In addition to work on features, I also did a few improvements on our development workflow. From automation scripts, through some helper methods for unit testing, to speeding up local build time by changing <a href="https://msdn.microsoft.com/en-us/library/ms164311.aspx">MSBuild verbosity</a> (printing to console takes time, in some cases we saved up to 1 minute of build time thanks to this simple trick!).</p>
<h3>Speaking, traveling, conferences</h3>
<p><img class="aligncenter size-full wp-image-15361" src="{{ site.baseurl }}/assets/2016/09/NDC_London_2016.jpg" alt="NDC London 2016" width="800" height="600" /></p>
<p>&nbsp;</p>
<p>Over the last year I have <a href="http://jj09.net/speaking/">spoken at a few conferences</a>, <a href="http://jj09.net/seattle-code-camp-aurelia-and-tdd-with-typescript-angularjs-and-node-js/">Seattle Code Camp</a>, and gave a talk at <a href="http://jj09.net/speech-recognition-in-the-browser-at-seattlejs/">SeattleJS meetup</a>.</p>
<p>I've been speaking mostly about <a href="http://jj09.net/building-large-scale-web-applications-with-typescript/">TypeScript</a>, <a href="http://jj09.net/azure-portal-the-largest-single-page-app-in-the-world/">Azure Portal</a> and <a href="http://jj09.net/seattle-code-camp-aurelia-and-tdd-with-typescript-angularjs-and-node-js/">Aurelia Framework</a> (yes - the last one is totally not related to my day job).</p>
<p>My most recent talk about the <a href="http://jj09.net/azure-portal-the-largest-single-page-app-in-the-world/">Azure Portal architecture</a> received a lot of great feedback. One gentleman told me that it was the best talk of the <a href="https://vslive.com/redmond">VSLive Redmond</a> conference, somebody <a href="https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-Live-Redmond-2016/T15">wrote a comment that it was the "Most interesting non-scotthanselman presentation ever"</a>, and one person mentioned it (as "excellent talk") in <a href="https://feedback.azure.com/forums/223579-azure-portal/suggestions/5048221-open-source-the-portal-blade-tech">Azure Portal user voice</a> (which I found while writing this post and searching for a link to <a href="https://feedback.azure.com/forums/223579-azure-portal/suggestions/5048221-open-source-the-portal-blade-tech">Open Source Portal UI user request</a> for previous section).</p>
<p>Over last year I learned that going to talks at the conferences is the least important thing. The most important is to connect with people from outside of your everyday work environment, share experiences, and networking. The most interesting conversations don't happen during the presentations, but at the post conference dinner or after party. I really recommend to read chapter 14 of <a href="https://www.amazon.com/Never-Eat-Alone-Expanded-Updated/dp/0385346654">Never Eat Alone</a> before attending a conference!</p>
<p>When I am telling people that I travel around the World to speak at conferences, they think it looks like this:</p>
<p><img class="aligncenter size-full wp-image-15311" src="{{ site.baseurl }}/assets/2016/09/conferences_WolfOfWallStreet.png" alt="conferences wolf of wall street" width="640" height="272" /></p>
<p>They forgot that most of the time it looks like that:</p>
<p><img class="aligncenter size-full wp-image-15321" src="{{ site.baseurl }}/assets/2016/09/conferences_travel.jpg" alt="conferences - travel" width="565" height="190" /></p>
<p>Of course there are pros and cons.</p>
<p>Pros:</p>
<ul>
<li>Learning new things (while preparing your talk, and during the conference from others).</li>
<li>Meeting new people</li>
<li>Visiting places you haven't been before. On my way to NDC London I paid from my own pocket for flight through Iceland with 34 hours connection flight in Reykjavik. I managed to see <a href="http://www.iheartreykjavik.net/2014/12/drive-it-yourself-the-golden-circle/">the Golden Circle</a>, attend <a href="https://www.google.com/search?q=harpa+concert+hall&amp;rlz=1C1CHFX_enUS606US606&amp;tbm=isch&amp;tbo=u&amp;source=univ&amp;sa=X&amp;ved=0ahUKEwi8-vvWm__OAhUL2mMKHb1jA54QsAQIPw&amp;biw=2327&amp;bih=1301">New Year's Concert at Harpa</a>, and <a href="https://www.instagram.com/p/BAXUPGTHttI/">I've seen the Northern Lights</a>. I have also seen a little bit of London during the same trip</li>
</ul>
<p>Cons:</p>
<ul>
<li>You need to work after hours to learn and prepare talk for the conference. You also need to write a good abstract so you talk will be selected. This takes a lot of time!</li>
<li>Travelling to conference takes time that you could spend with friends, family, or riding bike. Even if it is domestic flight it takes ~30 mins to get to airport, then ~2 hours on airport, ~2-4h during the flight, ~30 mins to get to the hotel etc. When it is on the other continent then you waste even more time + get jet lag. Oh...and you need to pack day before (~30 mins to 1 hour), and you don't have your nice 3 monitor setup and comfortable Herman Miller chair for a few days.</li>
<li>Sometimes you don't see anything except airport, aircraft, hotel and conference venue (that was the case when I went to <a href="http://jj09.net/connectjs-and-all-things-open/">ConnectJS conference in Atlanta</a> and <a href="http://jj09.net/open-source-at-microsoft-and-beyond/">Open Source North in Minneapolis</a>).</li>
</ul>
<p>Thanks to speaking at conferences, I met a lot of interesting people, and definitely expanded my knowledge. What's important: I learned the most during one on one conversations in the hallway or at the conferences' dinners.</p>
<p>In addition to conferences I was a guest at <a href="http://dotnetrocks.com">.NET Rocks podcast</a>, where <a href="http://jj09.net/net-rocks-podcast-building-the-azure-portal/">I talked about the Azure Portal</a>. I was also interviewed by <a href="http://davidgiard.com/">David Giard</a> - who I met at <a href="http://jj09.net/open-source-at-microsoft-and-beyond/">Open Source North conference</a> - for his <a href="https://channel9.msdn.com/Blogs/Technology-and-Friends/tf434">Technology and Friends series</a>. <a href="https://twitter.com/saraclay15">Sara Clayton</a> - who works on Open Source at Microsoft, and who I met at the <a href="http://jj09.net/connectjs-and-all-things-open/">All Things Open conference</a> - did an <a href="https://medium.com/open-at-microsoft/jakub-software-engineer-microsoft-c7cdfa0ff0de#.lm38rmogx">interview with me about my Open Source library</a>: <a href="https://github.com/jj09/voiceCmdr">voiceCmdr</a>. <a href="http://www.codefoster.com/">Jeremy Foster</a> (who I met at <a href="http://jj09.net/speech-recognition-in-the-browser-at-seattlejs/">SeattleJS meetup</a>) did an interview with me for his <a href="https://channel9.msdn.com/niners/codefoster">CodeChat show</a> (episode coming soon).</p>
<h3>Learning</h3>
<p><img class="aligncenter size-full wp-image-8291" src="{{ site.baseurl }}/assets/2016/09/workspace.jpg" alt="workspace" width="1200" height="553" /></p>
<p>Over the last year I've learned a lot about web development, performance, and accessibility. A lot of things I learned are captured in <a href="http://jj09.net/azure-portal-the-largest-single-page-app-in-the-world/">my last talk about the Azure Portal</a>. I improved my coding skills, debugging skills, and also - mainly thanks to attending conferences - communication skills, which is very important in Software Engineer portfolio.</p>
<p>In <a href="http://jj09.net/my-first-year-at-microsoft/">my first year review</a> I forgot to mention Microsoft Library, which is one of my favorites benefits at Microsoft. <a href="https://www.goodreads.com/review/list/28888194?order=d&amp;shelf=read&amp;sort=date_read">Most books I have read over last 2 years</a> are from MS Library. I <a href="http://jj09.net/tag/book-review">reviewed a few of them</a>, and some landed in <a href="http://jj09.net/books/">my favorite books list</a>. <a href="http://jj09.net/why-you-should-read-the-pragmatic-programmer/">The Pragmatic Programmer</a> book said that you should read a technical book every quarter.</p>
<p>Last time, I also didn't mention that when you are working on something related to Cloud, you have to be <a href="http://www.scientificamerican.com/article/the-strain-of-always-being-on-call/">on-call</a> once for a while. I am very lucky, because our team is large, and rotation requires everybody to be on-call only 1 week per 6-7 months. I have some friends who are on-call one of every three weeks, or even every other week (sic!). FYI - being on call means:</p>
<ul>
<li>no flexible work schedule</li>
<li>no freedom (you need to be able to act on incident right away = you need to be close to your computer and Internet = you don't go hiking, you don't go out with friends, you don't go for a bike ride)</li>
<li>I don't know what can be worse than your phone ringing at 4 am, and some people asking you for help with investigating some problem they cannot solve (hint: these people are not stupid, the problem is hard, your brain usually do not work the best in the middle of the night)</li>
</ul>
<p>However, there are also a good things in being on-call:</p>
<ul>
<li>you can learn more about the project (when you need to investigate/diagnose something in the area you are not familiar with)</li>
<li>you can improve your debugging/investigating/diagnosing skills</li>
<li>you can meet new people across the company</li>
</ul>
<p>The new thing for me, over last 12 months, was conducting interviews. It was very interesting experience. The most important thing I've learned was to never skip the coding question. My interview usually contains 3 parts:</p>
<ol>
<li><span style="line-height: 1.5;">chat about candidate previous projects/experience</span></li>
<li>easy coding question</li>
<li>design question</li>
</ol>
<p>There will be more details in upcoming blog post, but if you are interviewing people, I really recommend you to check out <a href="http://www.joelonsoftware.com/articles/GuerrillaInterviewing3.html">The Guerrilla Guide to Interviewing (version 3.0) by Joel Spolsky</a>.</p>
<h3>Staying fit and healthy</h3>
<p><img class="aligncenter size-full wp-image-14531" src="{{ site.baseurl }}/assets/2016/09/run.jpg" alt="Jakub Jedryszek - run" width="800" height="533" /></p>
<p>When you are developer, you <a href="http://blog.debugme.eu/the-healthy-web-developer/">need to take care of your health</a>. Sitting 10+ hours is not good for you. <a href="http://www.huffingtonpost.com/the-active-times/sitting-is-the-new-smokin_b_5890006.html">Sitting is the new smoking</a>. Additionally it turns out that <a href="http://getupandcode.com/2013/11/08/get-up-and-code-27-talking-about-the-healthy-programmer-with-joe-kutner/">staying fit and healthy makes you better developer</a>.</p>
<p><a href="https://www.strava.com/athletes/10257149">I bike</a>, <a href="https://www.strava.com/athletes/10257149">I swim</a>, <a href="https://www.strava.com/athletes/10257149">I run</a>, I hike, I take part in bike rides (like <a href="https://www.cascade.org/rides-major-rides/group-health-stp-presented-alaska-airlines">206 miles Seattle to Portland</a>, or <a href="https://www.cascade.org/rides-major-rides/ride-seattle-vancouver-and-party-rsvp">180 miles Seattle to Vancouver</a>), and I compete in <a href="https://www.athlinks.com/athletes/269132092">triathlons</a> once for a while.</p>
<p>Staying fit and healthy is not only about exercising. It is actually <a href="http://pledgetostayfit.com/all-in-one-nutrition-page">more about your diet</a>:</p>
<p><img class="aligncenter size-full wp-image-15411" src="{{ site.baseurl }}/assets/2016/09/exercise_diet.jpg" alt="exercise and diet chart" width="300" height="282" /></p>
<p>However, <a href="https://www.amazon.com/Hollywood-48-Hour-Miracle-Diet-32-Ounce/dp/B001G7QMQ2">diet-miracle</a> is not a way to go. Last year I tried to <a href="https://www.microsoft.com/microsoft-band/en-us/support/health-and-exercise/calories-burned">count calories I burn</a> and consume throughout the day, and develop a diet I would be able to sustain for a long term. The trick is to realize that it is not worth to eat some things. E.g., this <a href="http://community.babycenter.com/post/a48685555/calorie_q_could_1_cookie_have_500_calories">500 calories cookie</a> is not worth it. I would rather eat two <a href="http://www.myfitnesspal.com/food/calories/hersheys-symphony-giant-bar-6-8-milk-chocolate-almonds-toffe-166564539">Symphony bars from Hershey's</a>. Oh...and you need to wait for results couple of months or so.</p>
<p>It's great that Microsoft cafeterias now provide calorie counts in the food menu. I am not eating these burgers that are 1400 calories, but other ones that have only 700. Together with <a href="http://cdn.marketplaceimages.windowsphone.com/v8/images/8e04ec61-bbc7-4295-9cef-ccd2301f9f78?imageType=ws_screenshot_large&amp;rotation=0">Microsoft running trails</a> it provides a great fitness bundle.</p>
<p>There are also <a href="https://www.asahitechnologies.com/blog/tips-on-staying-fit-for-software-developers">other aspects you should take into account</a> to stay healthy.</p>
<p>Oh...and I forgot to mention another awesome Microsoft benefit: <a href="https://www.proclub.com">Pro Club gym</a> - one of the best gyms on the West Coast, and for sure the best in Seattle area. When I did a tour (right after I joined Microsoft 2 years ago), and the guy who was showing me around told me that they can service my car when I work out I was sure he was joking...<a href="https://www.proclub.com/Amenities/Auto-Salon">he wasn't</a>.</p>
<p><img class="aligncenter size-full wp-image-15291" src="{{ site.baseurl }}/assets/2016/09/pro_club.jpg" alt="PRO Club" width="800" height="449" /></p>
<h3>What next?</h3>
<p>Stay tuned!</p>

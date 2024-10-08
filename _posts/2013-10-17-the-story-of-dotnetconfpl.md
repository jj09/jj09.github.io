---
layout: post
title: The Story of dotNetConfPL
date: 2013-10-17 11:51:56.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- events
tags:
- ".NET"
- C#
- developer
- dotNetConfPL
- javascript
- lecture
- Open Source
- SublimeText
- windows phone
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  dsq_thread_id: '1868465005'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/the-story-of-dotnetconfpl/"
---
<p>It is all about people and cooperation!</p>
<h4>Long story short</h4>
<p>April 25-26 - <a href="http://dotnetconf.net">dotNetConf</a> took place, online conference for .NET developers, organized by <a href="http://www.hanselman.com">Scott Hanselman</a> and <a href="http://lozanotek.com/">Javier Lozano</a></p>
<p>April 27 - I text <a href="http://pawel.sawicz.eu/">Pawel Sawicz</a>, that we can organize something similar with Polish speakers and name it dotNetConf<strong>PL</strong>, he said: "it's a good idea". <b>(motivation++)</b></p>
<p>April 28 - Pawel told me that <a href="http://www.mfranc.com">Michal Franc</a> is also interested and we created google doc to write down ideas and todos. <b>(motivation++)</b></p>
<p>May 24 - We ask Scott Hanselman whether we can use dotNetConfPL as a name of the conference (because it's very similar to name of his conference). He and Javier Lozano confirmed in the same day and wished us good luck. <b>(motivation++)</b></p>
<p>June 6 - We sent e-mail to <a href="http://maciejaniserowicz.com/">Maciej Aniserowicz</a>, with a proposition to be a speaker at our conference.</p>
<p>June 7 - He responded: yes (we had first speaker!). <b>(motivation++)</b></p>
<p>After that, we were inviting rest of speakers and most of them accepted our invitations. We really appreciate this, because they didn't get any benefits from that.</p>
<p>July 14 - We announced dotNetConfPL on facebook and gain almost 50 registrations for the event within 1 hour! <b>(motivation++)</b></p>
<h4>The week of the conference</h4>
<p>A few days before the conference we did initial testing with speakers. To check, whether their microphone, resolution, etc. is set properly. Sometimes we had issues with Google Hangouts. Solution for that was simply disconnect and create a new 'hangout'. Our initial plan was to make only 1 hangout for entire conference, because each one has different link. We wanted to avoid forcing people to refresh the website or use of SignalR. However after that, we decided it will be better (safer and more flexible) to create separate 'hangouts' for each speaker and update link using SignalR.</p>
<p>Website for conference was created in ASP.NET MVC framework. The SignalR+CounchDB feature was implemented day before conference. After the conference I found interesting file in our solution:</p>
<p><img src="{{ site.baseurl }}/assets/2013/10/dotnetconfpl-code.png" alt="dotnetconfpl - code" width="589" height="385" class="aligncenter size-full wp-image-723" /></p>
<p>It is worth to mention that during the conference I was in Manhattan, KS, while Pawel and Michal were in Wroclaw, Poland. The image below, is my Command Center. ThinkPad X220 is connected with 2 monitors and through it I am connected to speakers. On MacBook I am connected via Skype with Michal and Pawel. On Surface I have live streaming (about 30 seconds delay) to be sure everything is working fine. The only issue I had, was not enough ears. I had only two: in one I was connected to the speaker, second - Michal and Pawel, and if I had third, I would be able to track the live streaming :)</p>
<p><img src="{{ site.baseurl }}/assets/2013/10/dotNetConfPL-center.jpg" alt="dotNetConfPL - center" width="800" height="598" class="aligncenter size-full wp-image-732" /></p>
<h4>Sessions</h4>
<p>All sessions were in Polish. If you don't speak Polish, you can mute the sound, play <a href="http://www.youtube.com/watch?v=sZHdYOBRpsk">this</a> in background and watch :) You won't get full experience, but still can get a lot from each session!</p>
<p>What is cool, all of them are for beginners and non-beginners in the same time. Which means, everybody will learn something from each session. Additionally: all of them are in HD (720p). Google enabled it by the end of August.</p>
<h6>Maciej Aniserowicz: Unit testing in .NET</h6>
<p>Maciej shows TDD live example. From nothing to well-tested communication with external API.</p>
<p><iframe width="640" height="360" src="//www.youtube.com/embed/gQaShMN_tN8?feature=player_embedded" frameborder="0" allowfullscreen></iframe></p>
<h6>Filip Wojcieszyn: scriptcs - C# on diet</h6>
<p>Filip shows how to use C# in Console and/or in SublimeText.</p>
<p><iframe width="640" height="360" src="//www.youtube.com/embed/d72N_ZyvlMA?feature=player_embedded" frameborder="0" allowfullscreen></iframe></p>
<h5>Jakub Gutkowski: JavaScript for C# developer</h5>
<p>Jakub shows differences between C# and JavaScript, and language flavors every developer should be aware of, which may cause hard to track bugs.</p>
<p><iframe width="640" height="360" src="//www.youtube.com/embed/kleyCHc8Ecw?feature=player_embedded" frameborder="0" allowfullscreen></iframe></p>
<h5>Tomasz Janczuk: Node.js, Edge.js and Windows Azure</h5>
<p>This session blew my mind (and not only mine). Edge.js allows you to mix Node.js, C#, F#, IronPython, PowerShell and T-SQL code in <strong><u>one</u></strong> file!</p>
<p><iframe width="640" height="360" src="//www.youtube.com/embed/jAU4d7nVTdU?feature=player_embedded" frameborder="0" allowfullscreen></iframe></p>
<h5>Maciej Grabek: Windows Phone 8 Tips & Tricks</h5>
<p>Maciej shows set of useful(8) tricks for WP8 developers. From displaying helper-grid during development, to how to get more ratings for your app. </p>
<p><iframe width="640" height="360" src="//www.youtube.com/embed/PdNnnRpKQkI?feature=player_embedded" frameborder="0" allowfullscreen></iframe></p>
<h4>Summary</h4>
<p>Everything went well. We didn't have any problems with streaming (thanks Google Hangouts) and website (thanks Windows Azure and SignalR). I noticed that sometimes, on my Surface RT, IE11 wasn't refreshing the link. But, come on...it's IE, so we can ignore it :)</p>
<p>We had room on JabbR for discussion and ask questions to speakers. For a few minutes, even David Fowler (one of SignalR developers) visited it.</p>
<p>I am very glad that many people attended the conference. We had more than 600 registrations, almost 100 people in JabbR room and around 100-200 online viewers. But many people were watching the conference together, and in this case 1 online viewer = more that 1 physical viewers.</p>
<div style="text-align: center">
<img src="{{ site.baseurl }}/assets/2013/10/dotNetConfPL-atCompany.jpg" alt="dotNetConfPL - atCompany" width="300" class="alignnone size-medium wp-image-725" /><br />
<img src="{{ site.baseurl }}/assets/2013/10/dotNetConfPL-pizza.jpg" alt="dotNetConfPL - pizza" width="300" class="alignnone size-medium wp-image-726" />
</div>
<p>Thank you very much for all speakers! You did a great job guys, all sessions are international level!<br />
Thanks to <a href="http://www.mfranc.com">Michal</a> and <a href="http://pawel.sawicz.eu">Pawel</a> for organizing this conference with me.<br />
Thanks to Scott Hanselman and Javier Lozano for inspiration.<br />
And...thank you very much for all of you who were watching the conference and spreading the news!</p>
<p><strong>EDIT:</strong><br />
Short list of tools/technologies we were using for the conference:</p>
<ul>
<li>Google Hangouts</li>
<li>ASP.NET MVC</li>
<li>SignalR</li>
<li>CouchDB</li>
<li>Windows Azure (to be able to scale the instance, depends on the number of users)</li>
<li>Google Docs (as a database for most important information)</li>
<li><a href="http://trello.com/">Trello</a> (for tasks management)</li>
<li><a href="http://appharbor.com/">AppHarbor</a> (as test server)</li>
</ul>

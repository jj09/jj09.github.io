---
layout: post
title: My first year at Microsoft
date: 2015-09-08 00:34:25.000000000 -07:00
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
  builder_switch_frontend: '0'
  dsq_thread_id: '4108627929'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/my-first-year-at-microsoft/"
---
<p>I joined Microsoft on September 8, 2014. Today is my first year anniversary.</p>
<p><img class="aligncenter size-full wp-image-10921" src="{{ site.baseurl }}/assets/2015/09/changing-the-world-with-hololens.jpg" alt="Changing the World with Holo Lens" width="800" height="420" /></p>
<h3>How do I get the job at Microsoft</h3>
<p>When I was in College/Grad School, I wanted to work for Microsoft, because of Scott Hanselman, Scott Guthrie, Steve Sanderson, Damian Edwards, Mads Kristensen, Anders Hejlsberg, Eric Lippert, and other great developers. However, I knew them only from their blogs, and conference talks. I didn't know how day-to-day work at Microsoft looks like. When I was organizing <a href="http://dotnetconf.pl">dotNetConfPL 2013</a> I talked to Tomasz Janczuk, who worked for Microsoft for over 12 years, and he told me that "it is definitely worth it to work for Microsoft if you want to learn how to make software". After that, I was sure, I wanted to work for Microsoft.</p>
<p>In 2013, recruiter from Microsoft came to my department at Kansas State University, and after collecting resumes, selected group of people for on-campus interviews. I was one of them. Two weeks later I had 30 minutes interview on campus. It was short 5 minutes introduction, and 25 minutes of coding. After a week I got an email informing me that I was recommended for the next round - on-site interview in Redmond. Two months later I flew from Manhattan, KS to Redmond, WA. Interview in Redmond was a set of 5 interviews, with 5 different people, 1 hour each. Every interviewer was asking briefly about myself, and then programming question. What was surprising for me, they asked me to write code in Visual Studio. Two weeks after the interview I got an offer, which I accepted and on September 2014 I joined the Azure Portal Team.</p>
<h3>What have I done during my first year</h3>
<p>I am working for the Azure Portal Framework team, which is delivering the core of the portal, and framework to build extensions on top of it. Each Extension, e.g. Websites, Virtual Machines, or Application Insights, is a gateway to underlying Azure infrastructure. Framework team is divided in a few subgroups. My group is responsible mainly for developing reusable controls that are part of the framework. I created a few controls, and I was fixing/improving some other. The most challenging one was to create a set of date/time controls. Why was it hard? Because <a href="http://jj09.net/javascript-date-a-bad-part/">JavaScript Date sucks</a>, and <a href="https://www.youtube.com/watch?v=-5wpm-gesOY">it is not easy to deal with date/time at all</a>.</p>
<p>In addition to controls, I was also working on keyboard support for the Portal, and keyboard shortcuts that I blogged about earlier this year (<a href="http://jj09.net/hidden-feature-of-the-azure-portal-keyboard-shortcuts/">here</a> and <a href="http://jj09.net/more-keyboard-shortcuts-and-better-focus-management-on-the-azure-portal/">here</a>). Now, it is possible to use the portal with keyboard only.</p>
<p>I also helped to improve our development experience. I proposed to add <a href="http://sinonjs.org/">Sinon.JS</a> to our testing tool-set, and helped to create strong-typed wrapper on top of it - <a href="https://github.com/jj09/TypeSinon">TypeSinon</a> (which was proposed by Steve Sanderson). In order to make our QUnit tests cleaner, I also proposed and integrated <a href="https://github.com/AStepaniuk/qunit-parameterize">QUnit Parametrize</a> plugin that works like <a href="http://www.nunit.org/index.php?p=testCase&amp;r=2.5"><em>TestCase</em> attribute in NUnit</a>. I did other small improvements, like helping to upgrade to TypeScript 1.5, and turning off verbose printing to the console during build - which saves a few dev-minutes everyday, and ultimately a few dev-hours or even days per year.</p>
<h3>Lessons learned</h3>
<p>The best thing about working at Microsoft is the opportunity to work with smart people, and learn from them. All developers working at Microsoft are this type of people who get things done. They do not like to talk too much about what they want to do, but they prefer doing it instead. I remember when once I was arguing with some people over the email that something should be than in one way, not the other. After a few e-mails one teammate told me: "If you really believe that something should be done in some way, do not argue with people, just do it". I also noticed that the best developers do not ask you to do something for them, but send out a Code Review instead.</p>
<p>In my team there is no fear to try new things. Do you want to use the latest version of TypeScript, <span style="text-decoration: underline;">in production</span>, one day before the release? One of my team leaders, personally, performed this upgrade. Do you want to introduce, a new tool? Usually, not a problem, but then you are responsible for it. When I wanted to add Sinon.JS, I sent an email to the entire team to ask what they think. A few folks had some doubts (not about if, but about how). We called a quick meeting, and resolved all of them. Next time, when I wanted to add QUnit Parametrize, I just sent out a Code Review and email to entire team. No problems, everybody was ok with that. The only price I have to pay is helping others with issues related to these libraries. "With great power comes great responsibility" :)</p>
<p>I also remember when I wanted to make some change and asked a few people if I can do it. Nobody was sure, and somebody said: "It's better to ask for forgiveness than for permission" :)</p>
<p>Even if you fail, or create something not perfect, people at Microsoft do not criticize very often saying: "This sucks, that sucks". They know these words would create an expectation to propose better solution, or even implement it, and then - in the future - be responsible for every issue related to that. Instead, they say: "what do you think about this alternative solution?", or "let's take a look if we can do it better", or do not say anything.</p>
<p>From development perspective, the most valuable lesson I learned was to avoid planning for one, big refactoring in the future (which usually you will never have time for), but instead perform small refactorings with every commit. I had also opportunity to observe the real value of tests in the project. Many times when somebody, or myself, were performing some change that "there was no way it could impacted that functionality", and test was failing - it saved us from probably many long hours of debugging and investigating. I could also observed when after a few weeks we noticed something wasn't working from "some time ago", and we didn't know what caused it because we didn't have tests. Every time when this happened we had to invest a lot of time to investigate and find the change that caused this (which is not easy in project where 40+ people contribute to one repository, and you have ~40 commits every day).</p>
<h3>Culture</h3>
<p>I have many friends who knows two things for sure:</p>
<ul>
<li>eventually they will die</li>
<li>corporations are evil</li>
</ul>
<p>I was afraid of the second. Especially after reading the stories about Microsoft on the Internet that can be summarized like that:</p>
<p><img class="aligncenter size-full wp-image-10801" src="{{ site.baseurl }}/assets/2015/09/microsoft-org-chart.jpg" alt="Microsoft org chart" width="600" height="389" /></p>
<p>The fact that there is enterprise overhead at Microsoft is true. It was nicely summarized by Eric Lippert in his blog post <a href="http://blogs.msdn.com/b/ericlippert/archive/2003/10/28/how-many-microsoft-employees-does-it-take-to-change-a-lightbulb.aspx">How many Microsoft employees does it take to change a lightbulb?</a> However, now Microsoft is becoming a cool company again. The idea of <a href="https://news.microsoft.com/2013/07/11/one-microsoft-company-realigns-to-enable-innovation-at-greater-speed-efficiency/">One Microsoft</a> is happening now. It feels like people are working towards the same goal. Last summer I participated in <a href="http://www.geekwire.com/2015/at-microsofts-hackathon-employees-come-up-with-solutions-to-fix-societal-problems/">//oneweek hackathon</a> where together with people from different teams across Microsoft we were hacking together, and it was great to be a hacker for a few days while being an engineer in everyday job (<a href="http://dandreamsofcoding.com/2013/09/16/hackers-and-software-engineers/">Hackers and Software Engineers</a>). Recently I was at IoT meetup in Seattle, and one guy said: "Microsoft was a wonderful company in 90', and then took a wrong direction in 2000', but now they are switching back. There is many interesting things happening at Microsoft now, and they are becoming cool again". Other people are starting notice this as well: <a href="http://seekingalpha.com/article/3135906-microsoft-is-cool-again">link</a>, <a href="http://www.usatoday.com/story/tech/2015/01/21/is-microsoft-cool-again-big-tech-push/22115289/">link</a>, <a href="http://www.theverge.com/2015/3/2/8134603/microsoft-is-cool-again">link</a>.</p>
<p>There is even a new, unofficial logo of the NEW Microsoft - Ninja Cat on Unicorn:</p>
<p><img class="aligncenter size-full wp-image-10841" src="{{ site.baseurl }}/assets/2015/09/new-microsoft-logo.jpg" alt="New Microsoft logo" width="800" height="463" /></p>
<p>I will say it again: there are many smart people working at Microsoft. What's more: higher in the hierarchy somebody is - he is a smarter person. This goes from my teammates, through our team leaders, all the way to Scott Guthrie and Satya. What is important when you work for some company, is to believe in your leadership team. I have no doubts that people like Scott Guthrie, Mark Russinovich or Satya know what they are doing. Additionally, every month there is Q&amp;A session with Satya, where every employee can ask him a question. I wish I could quote some of Satya's answers here, because they are really valuable, and reasonable pieces of advice. You can find more about Microsoft under Satya in <a href="http://www.wired.com/2015/01/microsoft-nadella/">this article</a>.</p>
<p>Let's also talk about management at the lower level. Many people in Microsoft says "my boss". I do not like calling my team leader like that, because I think he is more a leader than boss:</p>
<p><img class="aligncenter size-full wp-image-10831" src="{{ site.baseurl }}/assets/2015/09/boss-vs-leader.jpg" alt="boss vs leader" width="624" height="630" /></p>
<p>I have 1 on 1 with him on every week. Usually 30 minutes, sometimes less or more, depends on the needs. During these meetings he is checking how I am doing, and <u>how he can help me</u> with any issues I have, and how he can enable me to utilize my full potential. He is doing the same for other 8 developers in the team, and in addition to that, he is doing as much development as others. His scrum update is not much different than the rest of us.</p>
<p>Another interesting thing at Microsoft is separate hierarchy for developers and program managers. As Joel Spolsky pointed out in this book - Joel on Software - there is a reason behind it. Instead of giving direct orders to developer, program manager has to convince developer that whatever he want him to implement make sense.</p>
<h3>What next?</h3>
<p>It has been a great year. I had opportunity to work with amazing people, on a very interesting project, and I learned a lot.</p>
<p>I am staying with the Azure Portal team. We have a lot of work to do. Especially, because Azure is growing exponentially. One year ago, when you clicked 'Browse' on the portal, there was ~10 types of services on the list. Now, 1 year later, there is over 40 items on that list. This requires from us to enable other teams to develop at very fast pace using our framework. We keep improving the programming model, APIs, performance, and usability. There is also <a href="http://feedback.azure.com/forums/223579-azure-preview-portal">a lot of requests from users</a> that we constantly monitor, and make happen (150/739 are fulfilled for today). We really appreciate your feedback!</p>
<p>I am very excited about the future of the Azure Portal. From a developer point of view - it's a dream place to work. We are using the latest, greatest technologies. We are doing things that exercise browsers to such an extent that we are finding bugs in them, or have to fix/patch Open Source libraries that we are using. There is also a few features, I will be working on, that I am very excited about. Stay tuned!</p>
<p>Additionally, in upcoming months <a href="http://jj09.net/speaking/">I will be speaking at a few conferences</a>, and on October 31 there is the third edition of <a href="http://dotnetconf.pl">dotNetConfPL</a> - online conference for .NET developers that I co-founded together with <a href="http://www.mfranc.com">Michal Franc</a> and <a href="http://pawel.sawicz.eu">Pawel Sawicz</a>.</p>
<p>I would like to say thank you for every member of my team. It's a pleasure to work with you, and be part of Microsoft in these days. I has never been a better time to work for Microsoft!</p>

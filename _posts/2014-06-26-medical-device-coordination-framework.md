---
layout: post
title: Medical Device Coordination Framework
date: 2014-06-26 13:09:47.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
- studies
tags:
- AADL
- Ada
- BeagleBoard
- embeded
- Java
- Open Source
- SPARK
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  feature_size: blank
  builder_switch_frontend: '0'
  dsq_thread_id: '2797527344'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/medical-device-coordination-framework/"
---
<p><img class="aligncenter size-full wp-image-2981" src="{{ site.baseurl }}/assets/2014/06/patient-room-future.jpg" alt="Patient room - future" width="680" height="329" /></p>
<p>As a Research Assistant at <a href="http://santoslab.org">SAnToS Lab</a> I am working on <a href="http://mdcf.santos.cis.ksu.edu/">Medical Device Coordination Framework</a>. It is a long term research effort. MDCF is an implementation of <a href="http://www.mdpnp.org/mdice.html">Integrated Clinical Environment</a>. There is many people involved in it. Not only from my University. There are folks from University of Pennsylvania and some other researchers who cooperate with us. My part of research is focused on code translation. You can call it Model Driven Development. The long-term research goal is to create a <a href="http://en.wikipedia.org/wiki/Architecture_Analysis_%26_Design_Language">AADL</a>/<a href="http://link.springer.com/chapter/10.1007%2F978-3-642-38088-4_19#page-1">BLESS</a> to <a title="SPARK Ada programming language" href="http://jj09.net/spark-ada-programming-language/">SPARK Ada</a> translator for Medical Devices.</p>
<h3>Technologies</h3>
<p><a href="http://en.wikipedia.org/wiki/Architecture_Analysis_%26_Design_Language">AADL</a> stands for Architecture Analysis &amp; Design Language. It is modeling language, which allows to describe hardware and software parts of the system. It can be represented in graphical and textual form.</p>
<p><a href="http://link.springer.com/chapter/10.1007%2F978-3-642-38088-4_19#page-1">BLESS</a> stands for Behavioral Language for Embedded Systems with Software. It is an extension to AADL language. AADL can be extended by language annexes. BLESS is one of them. It is designed to prove embedded software/system conformance to specification. In other words: to verify the AADL model.</p>
<p><a href="http://spark-2014.org/">SPARK</a> is a programming language and static verification technology designed specifically for the development of high integrity software. It is subset of <a href="http://www.ada2012.org/">Ada</a> programming language. It contains all features of Ada, except:</p>
<ul>
<li>Pointers</li>
<li>Exceptions</li>
<li>Aliasing between variables</li>
<li>All Concurrency features</li>
<li>Side effects in expressions and functions</li>
</ul>
<p>However, it contains toolset for Software Verification, such as:</p>
<ul>
<li>Examiner - analyze code and ensures that it conforms to the SPARK language; also verify program to some extent using Verification Conditions (VC)</li>
<li>Simplifier - simplify Verification Conditions generated by Examiner</li>
<li>Proof Checker - prove the Verification Conditions</li>
</ul>
<p>I <a title="SPARK Ada programming language" href="http://jj09.net/spark-ada-programming-language/">blogged about SPARK Ada</a> recently.</p>
<h3>Research background</h3>
<p>The ultimate goal has a big scope. The goal is to deliver a platform, which allows different medical devices to work together. Moreover, there will be monitored and controlled by centralized system.</p>
<p>We use and create a lot of different technologies. From <a href="http://en.wikipedia.org/wiki/Architecture_Analysis_%26_Design_Language">AADL</a>, <a href="http://bless.santoslab.org/">BLESS</a>, <a href="http://mdcf.github.io/doc/dms/">DML</a> to <a title="SPARK Ada programming language" href="http://jj09.net/spark-ada-programming-language/">SPARK Ada</a>, Java, through many other. Most of them are still under development. I work mainly with AADL, BLESS and SPARK Ada. The biggest challenge for me is to understand how AADL models should be mapped to SPARK Ada in real-World. Unfortunately, I cannot find some Open Source examples on github. Companies treat it as their intellectual property, and do not share it. More over, the AADL committee still did not decide how some AADL constructs should be mapped to Software. Thus, my role is to propose it (based on existing work).</p>
<p>There is an AADL to Ada code generator: <a href="http://www.openaadl.org/ocarina.html">Ocarina</a>. It is written in Ada and it uses Ada features, which are not in SPARK language. However, it is a good point to start. Another resource I am based on is <a href="http://www.aadl.info/aadl/downloads/committee/feb2013/presentations/AADL_Code_Generation_Annex_draft0.8-20130127.pdf">Aerospace Standard - Architecture Analysis &amp; Design Language (AADL) V2 Programming Language Annex Document</a>. It describe data types translation and base for ports communication.</p>
<p>The essence of AADL models is port-based communication. Usually implemented in publish-subscribe mode. It allows to interaction between different components of the system.</p>
<h3>Sample medical device</h3>
<p>To create code translator for Medical Devices, I needed some example of Medical Device. One member of our research group, <a href="https://www.cis.ksu.edu/user/362">Brian Larson</a> created AADL/BLESS models of <a href="http://en.wikipedia.org/wiki/Patient-controlled_analgesia">Patient-controlled analgesia</a> Infusion Pump. This device, is used to infuse a pain killer. The dose can be controlled by patient. He also created <a href="http://santoslab.org/pub/open-pca-pump/artifacts/Open-PCA-Pump-Requirements.pdf">Open PCA Pump Requirements</a>. Document, which describe precisely functionalities of PCA Pump. My role is to develop AADL/BLESS to SPARK Ada translation schemes and translate existing PCA Pump models, to assure that translation makes sense.</p>
<p><a href="http://jj09.net/wp-content/uploads/2014/03/pca-pump.jpg"><img class="aligncenter size-medium wp-image-1156" src="{{ site.baseurl }}/assets/2014/06/pca-pump-225x300.jpg" alt="PCA Pump" width="225" height="300" /></a></p>
<h3>Research plan</h3>
<p>There are many issues and problems to solve in this project. One of them is SPARK limitation. Besides excluded features mentioned above, <a href="http://docs.adacore.com/spark2014-docs/html/lrm/tasks-and-synchronization.html">SPARK 2014 does not support multitasking</a> (yet). SPARK 2005 support it in some extent (with <a href="http://en.wikipedia.org/wiki/Ravenscar_profile">Ravenscar profile</a>). Thus I use mainly SPARK 2005.</p>
<p>The plan is as follows:</p>
<ul>
<li>Create AADL/BLESS to SPARK Ada translation schema</li>
<li>Manually implement working PCA-Pump prototype on <a href="http://jj09.net/beagleboard-your-personal-computer-smaller-than-your-wallet/">BeagleBoard-xM</a> based on Requirement document to find out possible implementation issues</li>
<li>Manually translate AADL/BLESS models to SPARK Ada, reusing code created during implementation</li>
<li>Create AADL/BLESS to SPARK Ada translator based on manual translated code</li>
</ul>
<h3>How it goes?</h3>
<p>I started working on this project around 1 year ago. Most of the time, I spend on studying AADL, SPARK Ada, BLESS and Ravenscar Profile. I thought, I would accomplish much more. However during the process I faced a lot of problems and I had to <a href="http://www.hanselman.com/blog/YakShavingDefinedIllGetThatDoneAsSoonAsIShaveThisYak.aspx">Shave the Yak</a>. First challenge was to run SPARK Ada code on <a title="BeagleBoard – your personal computer smaller than your wallet" href="http://jj09.net/beagleboard-your-personal-computer-smaller-than-your-wallet/">BeagleBoard-xM</a> device. In cooperation with Ada Core, we got cross-compiler, which works for its processor. It took around 3 months, because cross-compiler was under development. After around half a year of exploring, I came up with AADL ports translation schema (based on <a href="http://www.aadl.info/aadl/downloads/committee/feb2013/presentations/AADL_Code_Generation_Annex_draft0.8-20130127.pdf">AADL annex document</a>). Simultaneously, I was working on PCA Pump implementation (based on its <a href="http://santoslab.org/pub/open-pca-pump/artifacts/Open-PCA-Pump-Requirements.pdf">Requirements Document</a>). Most of it is described in <a href="http://jj09.net/wp-content/uploads/2014/06/SPARK-Ada-programming-for-ARM-based-deviceBeagleBoard-xM.pdf">SPARK Ada programming for ARM-based device(BeagleBoard-xM)</a>. It allowed me to better understand SPARK Ada development environment and create translation schemes for AADL packages threads. SPARK Ada development is much different than Java, C# or Python. After many hours spent on AADL/BLESS models analysis, I created mapping from BLESS to SPARK Ada.</p>
<p>For now, most of the work is done. Especially, translations schema. I have less than 2 months to finish everything. My plan is to refactor existing PCA Pump implementation and create final mock of code translated from AADL/BLESS models. Additionally I want to add implementation to some 'translated' part and apply SPARK Verification tools and AUnit tests. Finally, I will need to describe everything in my Master Thesis.</p>
<h3>My thoughts so far...</h3>
<p>Development for safety-critical systems is totally different, than creating Web or Mobile applications. My research adventure is very fascinating and allow me to discover new things everyday. It gives me different perspective of Software Development, which will be useful in the future. No matter if I would work for company producing Aircrafts or Space Shuttles. It will be valuable also for Web/Mobile Start-up in Silicon Valley or personal Mobile App. Finally I understand where UML and variety of Software Design Processes can be applied. Programming in SPARK Ada requires deep thinking and understanding about how every small part of the program work. There is no high abstraction layer, where calling some library function will do all work. It allows to understand what is underneath and how powerful languages like C#, Java or Python are.</p>
<p>If you are at the University now, I strongly recommend you to join some Research Group. Or at least talk to some of your professors and ask if you can do some Research-oriented project for him. No matter, if you are Graduate or Undergraduate student. If research topic is out of your comfort zone, then it is even better!</p>
<p><img class="aligncenter size-full wp-image-2971" src="{{ site.baseurl }}/assets/2014/06/outside-comfort-zone.png" alt="outside comfort zone" width="354" height="270" /></p>
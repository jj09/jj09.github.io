---
layout: post
title: Research Assistant Job - Project Sireum
date: 2013-08-08 12:05:07.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
- studies
tags:
- Ada
- Open Source
- pygtk
- python
- SPARK
meta:
  _yoast_wpseo_linkdex: '76'
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _yoast_wpseo_focuskw: sireum
  dsq_thread_id: '1585543715'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/research-assistant-job-project-sireum/"
---
<p>Since January 2013 I am Master student at Kansas State University. I am also Research Assistant at <a href="http://www.santoslab.org">SAnToS lab</a>.</p>
<h4>Bakar toolset</h4>
<p>Since the beginning I am working on project <a href="http://www.sireum.org">Sireum</a>. It is focused on toolset for analyzing Spark/Ada programs: <a href="http://www.sireum.org/bakar">Bakar</a>. Spark is subset of Ada programming language extended by code contracts. More info <a href="http://en.wikipedia.org/wiki/SPARK_(programming_language)">here</a>. Bakar contains two main tools: Alir (information flow analysis tool) and Kiasan (verification tool for code contracts). </p>
<p>The Kiasan tool is based on symbolic execution. Simply saying: it checks all possible code paths and discover possible issues (like variable overflow, side effects etc.). More info about Spark contracts can be found in <a href="http://www.adacore.com/sparkpro/tokeneer/discovery/">Tokeneer Discovery Tutorial</a>. Comprehensive description of Kiasan in contained in <a href="http://link.springer.com/content/pdf/10.1007%2F978-3-642-20398-5_6.pdf">this paper</a>.</p>
<h4>Kiasan plugin for GPS</h4>
<p>My first task was to integrate Kiasan tool (Java app) with <a href="http://libre.adacore.com/tools/gps/">GPS (GNAT Programming Studio)</a>. </p>
<p>I have never working on IDE plugins before. It was something totally new for me. That's why I was excited.</p>
<p>Plugins for GPS are written in PyGTK (Python graphic library). First I needed to learn <a href="http://jj09.net/python-jump-start/">Python and PyGTK</a>. Then I followed <a href="http://docs.adacore.com/gps-docs/users_guide/_build/html/index.html">GPS documentation</a> (especially chapters 16 and 18).</p>
<p>The sample flow of running Kiasan plugin is as follows:</p>
<ul>
<li>right click on method (which you want to analyze) and choose 'Run Kiasan'</li>
<li>handle this event and get method name and package name (will be needed to run Kiasan)</li>
<li>run external Java program (Kiasan.jar) from Python code (it has command line interface, so I just needed to execute <em>subprocess.call</em> method), which generates JSON report</li>
<li>parse JSON report and display it in the PyGTK window attached to the GPS</li>
<li>add code highlighting, dependent on chosen method or case (in report window by double-click)</li>
</ul>
<p>GPS along with Kiasan plugin is available in Sireum distribution, which can be downloaded from <a href="http://www.sireum.org/download">http://www.sireum.org/download</a>.</p>
<p>In the demo below I am showing how to install Sireum distribution and GPS with Kiasan plugin on Windows.</p>
<p><iframe width="640" height="360" src="http://www.youtube.com/embed/3Sh5_j3tqTk?feature=player_detailpage" frameborder="0" allowfullscreen></iframe></p>
<p>By the way: Sireum Project is <a href="http://github.com/sireum">Open Source on github</a>!</p>
<p>Do I like GRA job? Yes. It is very nice experience. I am able to work on Mac. I didn't have this opportunity before (I wouldn't buy it soon probably). I was able to learn Python (and PyGTK). I learn <a href="http://en.wikipedia.org/wiki/Design_by_contract">Design by Contract</a>. I learn how to create plugin for IDE (GNAT Programming Studio). We have continues integration server - Jenkins: I learn how to manage it. I explore the World of 'High Assurance Software' and Ada programming language, which is most common in such environment. It is totally different than working as software developer in some company. </p>
<p>Recently I started working on second SAnToS' project: <a href="http://mdcf.santos.cis.ksu.edu/">Medical Device Coordination Framework</a>. Another interesting thing. But I will tell you about it in another post.</p>
<p>Interesting fact: Ada programming language was named after <a href="https://en.wikipedia.org/wiki/Ada_Lovelace">Ada Lovelace</a> (1815–1852), who is credited as being the first computer programmer.</p>

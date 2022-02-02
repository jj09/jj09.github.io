---
layout: post
title: Garmin Programming Competition 2014
date: 2014-02-23 21:15:51.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- events
- programming
tags:
- algorithms
- bitbucket
- Eclipse
- git
- Java
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  dsq_thread_id: '2311247359'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/garmin-programming-competition-2014/"
---
<p>Yesterday at my university, <a href="http://www.garmin.com/">Garmin</a> was hosting the Programming Competition.</p>
<p>Competition like that is a great opportunity to practice programming, algorithms and problem solving skills. </p>
<p>We could form teams of 1-2 students. My partner was <a href="http://people.cis.ksu.edu/~danielwang/">Daniel Wang</a>. We could use following languages: C++, C#, Java and Python. We chose Java. We were using Eclipse IDE and git to share the code.</p>
<p>Organizers prepared very real-life <a href="http://jj09.net/wp-content/uploads/2014/02/GarminProgrammingCompetition2014.pdf">problems</a>. </p>
<p>Competitions had two parts:</p>
<ol>
<li>Read and perform simple input conversion (1 hour).</li>
<li>Reuse code from Program 1 and do more complicated operations with input (3 hours).</li>
</ol>
<p>We solved part 1 without any problems. Part 2 required two programs: 2A and 2B. We solved both, but our programs didn't pass all test cases. In 2A: 3/5 test cases passed, in 2B: 4/5. There were points for correct solution and bonus points (depended on the time when solution was submitted). Additionally, there was a timer showing how many bonus points we could earn sending solution now.</p>
<p>You can find problems description <a href="http://jj09.net/wp-content/uploads/2014/02/GarminProgrammingCompetition2014.pdf">here</a>. Our solutions are available on <a href="https://bitbucket.org/jj09/garmin-programming-competition-2014">Bitbucket repository</a>. Be aware that it is bad code, written under time pressure and never refactored. However, efficient enough to pass required time constraints. This is how you write code during programming contests :)</p>
<p>After competition we asked organizers about test input sets and they sent it to us. </p>
<p>This is the description of the bug we had and how we fix it (you can skip this part if you don't want to read the <a href="http://jj09.net/wp-content/uploads/2014/02/GarminProgrammingCompetition2014.pdf">description of problems</a>):</p>
<blockquote><p>The issue we had, was reading (shift mod 26) straight from the input file. Because e.g. shift = 45 should be effectively shift = 19 (45 mod 26). The program should stop when shift = 0. Then, when original shift was e.g. 52 we had stored shift=0 and we stopped (which was wrong). We thought that we should stop when the 'effective shift' is 0. Unfortunately, the test cases were stopping when the 'original shift' was 0. Fix was pretty easy (we just store two values: shift and shiftOrig for each cell). It would be very hard to fix this without test cases from organizers ;) It was like in real-life: small detail caused significant error.</p></blockquote>
<p>The challenge during programming competitions is that you cannot get all test cases. This time, there were 1 sample input per program. Which make sense, because otherwise everybody could just hardcode expected solution :) What is worse, you cannot see the program output (in case of runtime error). Fortunately, guys form Garmin were nice and when we asked, they were showing us the output (on their machine). It helped us (a lot) in fixing the runtime errors (during the competition).</p>
<p>The next event I am looking forward is <a href="https://code.google.com/codejam/"> Google Code Jam</a>. It starts in April 11, 2014 (Friday). Registration begins in March 11. I really encourage you to sign up. You can learn what various problems you can face and what you should consider during writing your programs. Additionally you can practice, apply your programming skills and compete with the best programmers in the World.</p>

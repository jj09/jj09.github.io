---
layout: post
title: Regular Expression Translator
date: 2014-05-13 19:19:01.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
- studies
tags:
- Antlr
- RegExp
- Scala
- unit tests
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _syntaxhighlighter_encoded: '1'
  feature_size: blank
  builder_switch_frontend: '0'
  dsq_thread_id: '2683247483'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/regular-expression-translator/"
---
<p>Another class I am taking this semester (except Real-Time Systems which I <a title="FreeRTOS Jump Start" href="http://jj09.net/freertos-jump-start/">blogged</a> about) is Formal Language Theory. It is very theoretical course. Most of the time is spend on formal proofs. Fortunately, one programming assignment was very fun.</p>
<p>The goal was to implement the program, which checks if one regular expression is subset of another. Thus, the input is two regular expressions.</p>
<p><img class="size-full wp-image-2031 alignright" src="{{ site.baseurl }}/assets/2014/05/RegExAutomatas.jpg" alt="RegEx Automatas" width="450" height="400" />The program use basic regular expressions notation and supports following operators:</p>
<ul>
<li>+ (union)</li>
<li>* (Kleene closure)</li>
<li>ε (Epsilon, empty expression)</li>
<li>0,1,2 (literals)</li>
</ul>
<p>To solve the problem, I had to take advantage of finite automatas (<a href="http://en.wikipedia.org/wiki/Nondeterministic_finite_automaton_with_%CE%B5-moves">ε-NFA</a> and <a href="http://en.wikipedia.org/wiki/Deterministic_finite_automaton">DFA</a>) in following order:</p>
<ol>
<li>Parse regular expressions E1 and E2</li>
<li>Create ε-NFAs N1 and N2 using Visitor pattern and transition described <a href="http://www.csee.umbc.edu/~squire/cs451_l6.html">here</a></li>
<li>Convert ε-NFAs N1 and N2 to DFAs D1 and D2 based on <a href="http://fleder44.net/312/notes/26_converting_nfa/index.html">this</a></li>
<li>Create D'I DFA, which is intersection of D1 and D2 DFAs generated in step 3</li>
</ol>
<h3>Implementation details</h3>
<p>Tools/Technologies:</p>
<ul>
<li>Eclipse</li>
<li>Scala</li>
<li>Java</li>
<li>ANTLRWorks 2</li>
<li>Scala JUnit tests</li>
</ul>
<p>I took advantage of ANTLR for parsing. I want to learn Scala and I am using it for every programming assignment in this semester if possible. ANTLRWorks 2 does not support Scala (it does not generate parser/lexer/visitor in Scala). However, ANTLRWorks 2 generates Java and interoperability between Scala and Java is easy. I decided to try it!</p>
<p>Scala is a main language in which this application was developed. ANTLRWorks 2 was used for parsing regular expression. The new version (v.2) generates <a href="http://www.oodesign.com/visitor-pattern.html">Visitor</a> class, which enables iterating through AST (Abstract Syntax Tree) nodes and perform appropriate actions. As I mentioned, ANTLRWorks 2 does not generate Scala code yet. Thus the generated parser and Visitor is in Java language.</p>
<p>During the intersection of DFAs creation, there is an exception thrown in 2 cases:</p>
<ul>
<li>There exists some node of newly created D’I DFA, which is sum of D1 final node and D2 <span style="text-decoration: underline;">not</span> final node</li>
<li>Some transition, which exists in D1 leads to dead node in D2</li>
</ul>
<p>Exception contains string, which is accepted by L(E1), but not by L(E2). Then, this string is returned as a result of execution. If no exception was thrown, it means, every final state of D1 is also final state of D2. That means L(E1) ∈ L(E2) and 'true' is returned.</p>
<h3>Running program</h3>
<p>The main program is Main.scala. You can find there String variables defined with sample Regular Expressions. The easiest way is to replace them (if you want to test different ones). You can also read input from the console (by commenting and uncommenting appropriate lines).</p>
<p>Empty regular exception cause Exception throw.</p>
<p>There is also set of unit tests to test some regular expressions. You are more than welcome to add new Unit tests if you want to.</p>
<h3>Input</h3>
<p>Every closure has to have parenthesis: (exp)*<br />
Union also require parenthesis and multiple unions are allowed: (exp1+exp2+exp3)<br />
Sample inputs:</p>
<ul>
<li>(0+1+2)*</li>
<li>((0(0+2)*+1)*+2)</li>
<li>((0(0+2)*+1)*+2+12+(00+21)*+0000110102)</li>
</ul>
<p>Details about accepted input can be found in <a href="https://github.com/jj09/RegExpTranslator/blob/master/RegExpTranslator/src/parser/RegEx.g4">ANTLR grammar file</a>.</p>
<h3>Summary</h3>
<p>In this assignment I was able to reuse my knowledge about compilers, learnt last semester in <a href="http://jj09.net/compilers-course-i-had/">Compilers course I had</a>. Additionally I had to implement automata representation and apply recursion to accomplish required tasks.</p>
<p>It is very simple translator. Handle only basic regular expressions and small language (only 0,1,2 literals allowed). However, the goal was to practice and understand how Regular Expressions work internally.</p>
<p>You can check the code of my translator on github: <a href="https://github.com/jj09/RegExpTranslator">RegExpTranslator</a>.</p>

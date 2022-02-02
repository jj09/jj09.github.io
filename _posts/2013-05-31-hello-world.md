---
layout: post
title: Hello (blog) World!
date: 2013-05-31 23:16:55.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- blog
tags:
- blog
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
  dsq_thread_id: '1498549603'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/hello-world/"
---
<p>Hi All!</p>
<p>My name is Jakub Jedryszek. There are many reasons why I start this blog. One of them is <a href="http://java.dzone.com/articles/ghost-who-codes-how-anonymity">this article</a>. The other one is the willingness to share my thoughts with the World. Thanks to <a href="http://mfranc.com/">Michal Franc</a> for a motivation :)</p>
<p>I created Hello World in couple of languages using <a href="http://wordpress.org/plugins/crayon-syntax-highlighter/">Crayon Syntax Highlighter</a> (code in C#, Ruby, Python, Java and C) and <a href="http://wordpress.org/plugins/syntaxhighlighter/">SyntaxHighlighter Evolved</a> (code in PHP). Please comment which syntax highlighter are you using and why.</p>
<p>C#:</p>
<pre class="theme:vs2012 lang:c# decode:true">Console.WriteLine("Hello (blog) World!");</pre>
<p>Ruby:</p>
<pre class="toolbar:2 lang:ruby decode:true">puts 'Hello (blog) World!'</pre>
<p>Python:</p>
<pre class="theme:github toolbar:1 lang:python decode:true">print 'Hello (blog) World!'</pre>
<p>Java:</p>
<pre class="theme:eclipse lang:java decode:true">System.out.println("Hello (blog) World!");</pre>
<p>C:</p>
<pre class="theme:twilight lang:c decode:true">main()
{
    printf("Hello (blog) World!");
}</pre>
<p>PHP:</p>
<p>[php]&lt;?php echo &quot;Hello (blog) World!&quot;; ?&gt;[/php]</p>
<p>Assembler (AT&T syntax):</p>
<pre class="theme:arduino-ide lang:asm toolbar:2 decode:true ">        .section        .rodata
string:
        .ascii "Hello (blog) World!\n"
length:
        .quad . -string         #Dot = 'here'
 
        .section        .text
        .globl _start           #Make entry point visible to linker
_start:
        movq $4, %rax           #4=write
        movq $1, %rbx           #1=stdout
        movq $string, %rcx
        movq length, %rdx
        int $0x80               #Call Operating System
        movq %rax, %rbx         #Make program return syscall exit status
        movq $1, %rax           #1=exit
        int $0x80               #Call System Again</pre>

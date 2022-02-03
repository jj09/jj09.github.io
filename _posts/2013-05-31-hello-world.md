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
{% highlight csharp %}
Console.WriteLine("Hello (blog) World!");
{% endhighlight %}
<p>Ruby:</p>
{% highlight ruby %}
puts 'Hello (blog) World!'
{% endhighlight %}

<p>Python:</p>
{% highlight python %}
print 'Hello (blog) World!'
{% endhighlight %}

<p>Java:</p>
{% highlight java %}
System.out.println("Hello (blog) World!");
{% endhighlight %}

<p>C:</p>
{% highlight c %}
main()
{
    printf("Hello (blog) World!");
}
{% endhighlight %}

<p>PHP:</p>
{% highlight php %}
<?php 
    echo "Hello (blog) World!"; 
?>
{% endhighlight %}
<p>Assembler (AT&T syntax):</p>
{% highlight asm %}
        .section        .rodata
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
        int $0x80               #Call System Again
{% endhighlight %}

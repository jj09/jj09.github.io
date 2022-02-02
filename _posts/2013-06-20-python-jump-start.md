---
layout: post
title: Python jump start
date: 2013-06-20 18:38:04.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- pygtk
- python
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
  _yoast_wpseo_metadesc: 'How to learn Python: tutorials, videos and resources'
  dsq_thread_id: '1510270117'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/python-jump-start/"
---
<p>In my current job (Research Assistant at <a href="http://www.santoslab.org/">SAnToS lab</a>) I had to learn Python. I was very happy because of that. It gaves me an opportunity to get familiar with one of the most popular programming languages nowadays. </p>
<p>I was very lucky to find awesome <a href="http://developers.google.com/edu/python/">Google's Python Class</a> by <a href="http://www-cs-faculty.stanford.edu/~nick/">Nick Parlante</a>. It is great! If you want to start programming with Python or just learn it for fun, start with this tutorial!</p>
<p>As a supplement to above course you can read some more detailed tutorial. I went through two: <a href="http://learnpythonthehardway.org/book/">Learn Python The Hard Way</a> and <a href="http://docs.python.org/2/tutorial/index.html">Tutorial from Python documentation</a>. However if you already know some other programming language(s), your should learn during development. Python contains almost all common features of programming languages such as if/else, loops, exceptions, functions, classes etc. I said 'almost', because there is e.g. no <em>switch</em> instruction. However to check things like that there is very well written <a href="http://docs.python.org/">documentation</a>. It contains a lot of examples. The main difference between other popular languages like (C, C# or Java) and Python is that there is no semicolons. We use colons and indentation instead.</p>
<p>[python]if number &gt; 0:<br />
  print &quot;This is natural number.&quot;<br />
else:<br />
  print &quot;This is not natural number.&quot;[/python] </p>
<p>Python is dynamic, strongly typed programming language. It means type checking occurs during the run time, instead of compilation time. Programming in Python is a real pleasure. Sometimes you can explicitly put your mind into the code. That is because of high level of abstraction. E.g. file operations are so simple and intuitive. You do not need to remember any <em>StreamReaders</em> or <em>BufferedReaders</em> and bunch of functions for simple I/O operations. Below example reads content of file.</p>
<p>[python]f = open('file.txt')<br />
f.read()<br />
f.close()[/python]</p>
<p>Cool feature is the possibility to call functions explicitly on string. Like that:</p>
<p>[python]&quot;jakub&quot;.upper()[/python] </p>
<p>There is a lot of implemented (widely used) functions in Python. As a comparison, let's see how to reverse words in a sentence using C, Java and Python.</p>
<p>In C:</p>
<p>[c]void reverse_words(char *sentence)<br />
{<br />
   char *start = sentence;<br />
   char *end = sentence;</p>
<p>   while (*end != '&#92;&#48;') {<br />
      ++end;<br />
   }<br />
   --end;</p>
<p>   reverse_chars(start, end);</p>
<p>   while (*start != '&#92;&#48;') {<br />
      for (; *start != '&#92;&#48;' &amp;&amp; *start == ' '; start++) ;<br />
      for (end=start; *end != '&#92;&#48;' &amp;&amp; *end != ' '; end++) ;<br />
      --end;<br />
      reverse_chars(start, end);<br />
      start = ++end;<br />
   }<br />
}</p>
<p>void reverse_chars(char *left, char *right)<br />
{<br />
   char temp;</p>
<p>   while( left &lt; right) {<br />
      temp = *left;<br />
      *left = *right;<br />
      *right = temp;<br />
      ++left;<br />
      --right;<br />
   }<br />
}[/c]</p>
<p>In Java:</p>
<p>[java]<br />
public string ReverseWords(string sentence)<br />
{<br />
  string[] words =  sentence.split(&quot; &quot;);<br />
  string rev = &quot;&quot;;<br />
  for(int i = words.length - 1; i &gt;= 0 ; i--)<br />
  {<br />
    rev += words[i] + &quot; &quot;;<br />
  }<br />
  return rev;<br />
}[/java]</p>
<p>In Python:</p>
<p>[python]def reverse_words(sentence):<br />
  return &quot; &quot;.join(reversed(sentence.split(&quot; &quot;)))[/python]</p>
<p>That's why Python is good for Rapid Development.</p>
<p>I am also using PyGTK (graphic library for Python) in my work. There is a great tutorial <a href="http://www.youtube.com/view_play_list?annotation_id=annotation_20612&feature=iv&p=7604BFACE2442F9A&src_vid=3z3NMkqBCZ8">Python GTK</a> on youtube! PyGTK requires very less code than e.g. C# to create some simple application. We do not to have tons of generated code when we start. We create application from scratch. Look at below Hello World example.</p>
<p>[python]import pygtk<br />
pygtk.require('2.0')<br />
import gtk</p>
<p>class HelloWorld:<br />
    def hello(self, widget, data=None):<br />
        print &quot;Hello World&quot;</p>
<p>    def destroy(self, widget, data=None):<br />
        gtk.main_quit()</p>
<p>    def __init__(self):<br />
        self.window = gtk.Window(gtk.WINDOW_TOPLEVEL)<br />
        self.window.connect(&quot;destroy&quot;, self.destroy)<br />
        self.window.set_border_width(10)<br />
        self.button = gtk.Button(&quot;Hello World&quot;)<br />
        self.button.connect(&quot;clicked&quot;, self.hello, None)<br />
        self.window.add(self.button)<br />
        self.button.show()<br />
        self.window.show()</p>
<p>    def main(self):<br />
        gtk.main()</p>
<p>if __name__ == &quot;__main__&quot;:<br />
    hello = HelloWorld()<br />
    hello.main()[/python]</p>
<p>The result is the window with button 'Hello World'. When you click the button, then 'Hello World' will be printed on console. All of that with 22 lines of code (I do not count white lines).</p>
<p><img src="{{ site.baseurl }}/assets/2013/06/hello_python.png" alt="Hello Python" width="341" height="208" class="alignnone size-full wp-image-216" /></p>
<p>If you don't know python yet, I encourage you to try it. Programming in python requires a little bit different way of thinking. It also allows you to look at the programming from the different perspective. </p>
<p>Python installation is easy on all operating systems and you can find it in google. To install PyGTK in Windows you can use <a href="http://ftp.gnome.org/pub/GNOME/binaries/win32/pygtk/2.24/">all in-one installer</a>. There is also <a href="http://sourceforge.net/projects/macpkg/files/PyGTK/2.24.0/PyGTK.pkg/download">all-in-one installer for Mac</a>. PyGTK is included in most Linux distributions, so you won't need to install it if you are using Linux.</p>

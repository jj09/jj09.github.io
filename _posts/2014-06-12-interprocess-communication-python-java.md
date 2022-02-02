---
layout: post
title: Interprocess communication between Python and Java
date: 2014-06-12 11:10:53.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- Java
- python
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
  _syntaxhighlighter_encoded: '1'
  builder_switch_frontend: '0'
  dsq_thread_id: '2758801500'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/interprocess-communication-python-java/"
---
<p>For my <a title="Research Assistant Job – Project Sireum" href="http://jj09.net/research-assistant-job-project-sireum/">Research work</a> I need to communicate between Python and Java/Scala application.</p>
<p>The first idea was to use WebSockets. It is universal and flexible. Additionally communication is easy. There are many ways to implement it:</p>
<ul>
<li><a href="https://ws4py.readthedocs.org/en/latest/">ws4py - A WebSocket package for Python</a></li>
<li><a href="http://www.codestance.com/tutorials-archive/python-tornado-web-server-with-websockets-part-i-441">Python Tornado Web Server With WebSockets</a></li>
<li><a href="https://pypi.python.org/pypi/websocket-client/0.15.0">websocket-client 0.15.0</a></li>
<li><a href="https://gist.github.com/geoffb/616117">Super simple websockets client/server using Python</a></li>
</ul>
<p>Implementation would be easy, but we are using customized version of Python, which is included in <a href="http://libre.adacore.com/tools/gps/">GNAT Programming Studio</a>. Some libraries (required for WebSockets) are excluded (because of legal reasons) and we wouldn't be able to redistribute it along with missing packages. Thus, we decide to implement interprocess communication through pipes.</p>
<h3>From Python to Java</h3>
<p>The communication is one direction: from Python app to Java app. Every message is one line of text (ultimately: json format). E.g.: "text\r\n". To close communication, we send message: "x\r\n".</p>
<p>This is sample Java app, which write received messages to file result.txt:</p>
<p>[java]import java.io.*;</p>
<p>public class MyClass {<br />
	public static void main(String[] args) {<br />
		try {<br />
			BufferedReader bufferRead = new BufferedReader(new InputStreamReader(System.in));<br />
			PrintWriter writer = new PrintWriter(&quot;result.txt&quot;, &quot;UTF-8&quot;);<br />
			String s = bufferRead.readLine();<br />
			while(s.equals(&quot;x&quot;)==false) {<br />
				writer.println(s);<br />
				s = bufferRead.readLine();<br />
			}<br />
			writer.close();<br />
		} catch(IOException e) {<br />
			e.printStackTrace();<br />
		}<br />
	}<br />
}[/java]</p>
<p>And here is sample Python app, which sends messages to Java app:</p>
<p>[python]#!/usr/bin/python</p>
<p>import subprocess</p>
<p>p = subprocess.Popen([&quot;java&quot;, &quot;MyClass&quot;], stdin=subprocess.PIPE)<br />
p.stdin.write(&quot;First line\r\n&quot;)<br />
p.stdin.write(&quot;Second line\r\n&quot;)<br />
p.stdin.write(&quot;x\r\n&quot;) # this line will not be printed into the file[/python]</p>
<h3>From Java to Python</h3>
<p>We can also communicate in opposite direction: from Java app to Python app. To do that we just need to change reading to writing in Java app and writing to reading in Python app.</p>
<p>Change in Java app is simple: we just write to standard output.</p>
<p>[java]import java.io.*;</p>
<p>public class MyClass2 {<br />
	public static void main(String[] args) throws InterruptedException{<br />
		System.out.println(&quot;First msg&quot;);<br />
		System.out.println(&quot;Second msg&quot;);<br />
		System.out.println(&quot;x&quot;);<br />
	}<br />
}[/java]</p>
<p>In Python app we need to create stdout pipe and read instead of write:</p>
<p>[python]#!/usr/bin/python</p>
<p>import subprocess</p>
<p>p = subprocess.Popen([&quot;java&quot;, &quot;MyClass2&quot;], stdout=subprocess.PIPE)<br />
line = p.stdout.readline()<br />
while(line != &quot;x\n&quot;):<br />
	print line<br />
	line = p.stdout.readline()[/python]</p>
<p>In this scenario, both processes are managed by Python app. You can also do it in <a href="http://stackoverflow.com/questions/4112470/java-how-to-both-read-and-write-to-from-process-thru-pipe-stdin-stdout">opposite direction and invoke Python app from Java app</a>.</p>

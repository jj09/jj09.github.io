---
layout: post
title: 'Multithreading: C# vs. Java'
date: 2014-03-29 20:38:47.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- ".NET"
- C#
- Java
- multithreading
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
  dsq_thread_id: '2547606591'
  feature_size: blank
  builder_switch_frontend: '0'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/multithreading-csharp-vs-java/"
---
<p>In my <a href="http://jj09.net/multithreading-in-csharp/">pervious post</a> I described basic multithreading constructs in C#. Now, I would like to compare them to conforming constructs in Java. It might be useful for those of you, who has already created some multithreaded applications in Java, and would like to learn how to do the same in C#.</p>
<h3>Creating a new thread</h3>
<p>C#:<br />
[csharp]using System;<br />
using System.Threading;</p>
<p>class ThreadTest<br />
{<br />
  static void Main()<br />
  {<br />
    Thread t = new Thread (Method);<br />
    t.Start();<br />
  }</p>
<p>  static void Method()<br />
  {<br />
    Console.WriteLine(&quot;Thread started&quot;);<br />
  }<br />
}[/csharp]</p>
<p>Java:<br />
[java]public class Program {<br />
  public static void main(String[] args) {<br />
    ThreadClass t = new ThreadClass();<br />
    t.start();<br />
  }<br />
}</p>
<p>class ThreadClass extends Thread {<br />
  @Override<br />
  public void run() {<br />
    System.out.println(&quot;Thread started&quot;);<br />
  }<br />
}[/java]</p>
<h3>Waiting for another thread to finish</h3>
<p>C#:<br />
[csharp]using System;<br />
using System.Threading;</p>
<p>class ThreadTest<br />
{<br />
  static void Main()<br />
  {<br />
    Thread t = new Thread (Method);<br />
    t.Start();<br />
    t.Join(); //wait for thread t<br />
    Console.WriteLine(&quot;Created thread finished&quot;);<br />
  }</p>
<p>  static void Method()<br />
  {<br />
    Console.WriteLine(&quot;Started new thread...&quot;);<br />
    Thread.Sleep(1000);<br />
    Console.WriteLine(&quot;Finishing new thread...&quot;);<br />
  }<br />
}[/csharp]</p>
<p>Java:<br />
[java]public class Program {<br />
  public static void main(String[] args) {<br />
    ThreadClass t = new ThreadClass();<br />
    t.start();<br />
    try {<br />
      t.join(); //wait for thread t<br />
      System.out.println(&quot;Created thread finished&quot;);<br />
	} catch(InterruptedException e) {<br />
	  // handle exception<br />
	}</p>
<p>  }<br />
}</p>
<p>class ThreadClass extends Thread  {<br />
  @Override<br />
  public void run() {<br />
    System.out.println(&quot;Started new thread...&quot;);<br />
    try {<br />
      Thread.sleep(1000);<br />
    } catch(InterruptedException e) {<br />
      // handle exception<br />
    }<br />
    System.out.println(&quot;Finishing new thread...&quot;);<br />
  }<br />
}[/java]</p>
<h3>Accessing shared variable</h3>
<p>C#:<br />
[csharp]using System;<br />
using System.Threading;</p>
<p>class ThreadTest<br />
{<br />
  static readonly object locker = new object();<br />
  static int sharedVariable;</p>
<p>  static void Main()<br />
  {<br />
    Thread t = new Thread (Method);<br />
    t.Start();<br />
    lock(locker)<br />
    {<br />
      // sample operation<br />
      if(sharedVariable==0)<br />
      {<br />
        sharedVariable = 1;<br />
      }<br />
    }<br />
  }</p>
<p>  static void Method()<br />
  {<br />
    lock(locker)<br />
    {<br />
      // sample operation<br />
      if(sharedVariable&gt;0)<br />
      {<br />
        sharedVariable++;<br />
      }<br />
    }<br />
  }<br />
}[/csharp]</p>
<p>Java:<br />
[java]public class Program {<br />
  public static int sharedVariable;<br />
  public static final Object lock = new Object();<br />
  public static void main(String[] args) {<br />
    ThreadClass t = new ThreadClass();<br />
    t.start();<br />
    synchronized(lock)<br />
    {<br />
      //sample operation<br />
      if(sharedVariable==0) {<br />
        Program.sharedVariable = 1;<br />
      }<br />
    }<br />
  }<br />
}</p>
<p>class ThreadClass extends Thread {<br />
  @Override<br />
  public void run() {<br />
    synchronized(Program.lock) {<br />
      //sample operation<br />
      if(Program.sharedVariable&gt;0) {<br />
        Program.sharedVariable++;<br />
      }<br />
    }<br />
  }<br />
}[/java]</p>
<h3>Signaling</h3>
<p>C#:<br />
[csharp]using System;<br />
using System.Threading;</p>
<p>class ThreadTest<br />
{<br />
  static EventWaitHandle _waitHandle = new AutoResetEvent (false);</p>
<p>  static void Main()<br />
  {<br />
    new Thread (Waiter).Start();<br />
    Console.WriteLine(&quot;Wait for notification...&quot;);<br />
    _waitHandle.WaitOne();<br />
    Console.WriteLine(&quot;Notification received.&quot;);<br />
  }</p>
<p>  static void Waiter()<br />
  {<br />
    Thread.Sleep (1000);<br />
    Console.WriteLine(&quot;Sending notification...&quot;);<br />
    _waitHandle.Set();<br />
  }<br />
}[/csharp]</p>
<p>Java:<br />
[java]class Program<br />
{<br />
  public static void main(String[] args) {<br />
    ThreadClass t = new ThreadClass();<br />
    t.start();<br />
    System.out.println(&quot;Wait for notification...&quot;);<br />
    synchronized(t) {<br />
      try {<br />
        t.wait();<br />
      } catch(InterruptedException e) {<br />
        //handle exception<br />
      }<br />
    }<br />
    System.out.println(&quot;Notification received.&quot;);<br />
  }<br />
}</p>
<p>class ThreadClass extends Thread {<br />
  @Override<br />
  public void run() {<br />
  	try {<br />
      Thread.sleep(1000);<br />
    } catch(InterruptedException e) {<br />
      //handle exception<br />
    }<br />
    System.out.println(&quot;Sending notification...&quot;);<br />
    synchronized(this) {<br />
      notify();<br />
    }<br />
  }<br />
}[/java]</p>
<h3>Summary</h3>
<p>As we can see, threading constructs in both languages are very similar.</p>
<p>I put all above code in github repository: <a href="https://github.com/jj09/Threading-in-CSharp-vs-Java">Threading-in-CSharp-vs-Java</a>. </p>
<p>Do you think, there are some other fundamental examples, which should be mentioned in this post?</p>

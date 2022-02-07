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

C#:

{% highlight csharp %}
using System;
using System.Threading;</p>
class ThreadTest
{
  static void Main()
  {
    Thread t = new Thread (Method);
    t.Start();
  }
  static void Method()
  {
    Console.WriteLine("Thread started");
  }
}
{% endhighlight %}

Java:

{% highlight java %}
public class Program {
  public static void main(String[] args) {
    ThreadClass t = new ThreadClass();
    t.start();
  }
}
class ThreadClass extends Thread {
  @Override
  public void run() {
    System.out.println("Thread started");
  }
}
{% endhighlight %}

<h3>Waiting for another thread to finish</h3>
C#:

{% highlight csharp %}
using System;
using System.Threading;
class ThreadTest
{
  static void Main()
  {
    Thread t = new Thread (Method);
    t.Start();
    t.Join(); //wait for thread t
    Console.WriteLine("Created thread finished");
  }
  static void Method()
  {
    Console.WriteLine("Started new thread...");
    Thread.Sleep(1000);
    Console.WriteLine("Finishing new thread...");
  }
}
{% endhighlight %}

Java:

{% highlight java %}
public class Program {
  public static void main(String[] args) {
    ThreadClass t = new ThreadClass();
    t.start();
    try {
      t.join(); //wait for thread t
      System.out.println("Created thread finished");
    } catch(InterruptedException e) {
      // handle exception
    }
  }
}
class ThreadClass extends Thread  {
  @Override
  public void run() {
    System.out.println("Started new thread...");
    try {
      Thread.sleep(1000);
    } catch(InterruptedException e) {
      // handle exception
    }
    System.out.println("Finishing new thread...");
  }
}
{% endhighlight %}

<h3>Accessing shared variable</h3>
C#:

{% highlight csharp %}
using System;
using System.Threading;
class ThreadTest
{
  static readonly object locker = new object();
  static int sharedVariable;
  static void Main()
  {
    Thread t = new Thread (Method);
    t.Start();
    lock(locker)
    {
      // sample operation
      if(sharedVariable==0)
      {
        sharedVariable = 1;
      }
    }
  }
  static void Method()
  {
    lock(locker)
    {
      // sample operation
      if(sharedVariable > 0)
      {
        sharedVariable++;
      }
    }
  }
}
{% endhighlight %}

Java:

{% highlight java %}
public class Program {
  public static int sharedVariable;
  public static final Object lock = new Object();
  public static void main(String[] args) {
    ThreadClass t = new ThreadClass();
    t.start();
    synchronized(lock)
    {
      //sample operation
      if(sharedVariable==0) {
        Program.sharedVariable = 1;
      }
    }
  }
}
class ThreadClass extends Thread {
  @Override
  public void run() {
    synchronized(Program.lock) {
      //sample operation
      if(Program.sharedVariable > 0) {
        Program.sharedVariable++;
      }
    }
  }
}
{% endhighlight %}

<h3>Signaling</h3>
C#:

{% highlight csharp %}
using System;
using System.Threading;
class ThreadTest
{
  static EventWaitHandle _waitHandle = new AutoResetEvent (false);
  static void Main()
  {
    new Thread (Waiter).Start();
    Console.WriteLine("Wait for notification...");
    _waitHandle.WaitOne();
    Console.WriteLine("Notification received.");
  }
  static void Waiter()
  {
    Thread.Sleep (1000);
    Console.WriteLine("Sending notification...");
    _waitHandle.Set();
  }
}
{% endhighlight %}

Java:

{% highlight java %}
class Program
{
  public static void main(String[] args) {
    ThreadClass t = new ThreadClass();
    t.start();
    System.out.println("Wait for notification...");
    synchronized(t) {
      try {
        t.wait();
      } catch(InterruptedException e) {
        //handle exception
      }
    }
    System.out.println("Notification received.");
  }
}
class ThreadClass extends Thread {
  @Override
  public void run() {
  	try {
      Thread.sleep(1000);
    } catch(InterruptedException e) {
      //handle exception
    }
    System.out.println("Sending notification...");
    synchronized(this) {
      notify();
    }
  }
}
{% endhighlight %}

<h3>Summary</h3>
<p>As we can see, threading constructs in both languages are very similar.</p>
<p>I put all above code in github repository: <a href="https://github.com/jj09/Threading-in-CSharp-vs-Java">Threading-in-CSharp-vs-Java</a>. </p>
<p>Do you think, there are some other fundamental examples, which should be mentioned in this post?</p>

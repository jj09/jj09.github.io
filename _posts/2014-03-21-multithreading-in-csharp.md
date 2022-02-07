---
layout: post
title: Multithreading in C#
date: 2014-03-21 11:13:30.000000000 -07:00
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
- multithreading
- teched
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
  dsq_thread_id: '2477483764'
  _wp_old_slug: multithreading-csharp
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/multithreading-in-csharp/"
---
<p>Multithreading is one of the advanced topics in Computer Science. Every Developer, sooner or later will need to write some multithreaded application. It is definitely better to do it sooner, even just for exercise, than later.</p>
<p>Everyone who attend a University and got a CS degree had to write at least one concurrent application. Usually, in Java, as 'standard language for Universities'. At least that was in my case, and two Universities I attended (Wroclaw University of Technology and Kansas State). Many University-based resources from Google are in Java. Sometimes there is C/C++ used. That's my observation after googling.</p>
<p>As .NET Developer I was interested in multithreading in C#. One of the best sources about that is <a href="http://www.albahari.com/threading/">Threading in C#</a> by Joseph Albahari. It's an overview of all threading-related features in C#. In this post, I would like to make an overview of the most basic techniques: accessing shared resources and signaling.</p>
<h3>Basic locking</h3>
<p>The issues with threading are usually correlated with shared resources (e.g. variables). One thread can start modifying it, while in meantime another thread also start do that. Then, sometimes, we cannot predict the final state of the resource (value of variable). Moreover, in one execution it can be value set by thread #1 and in the other - by thread #2.</p>
<p>To solve this issue, we have constructs such as: <a href="http://en.wikipedia.org/wiki/Semaphore_(programming)">semaphors</a> or <a href="http://en.wikipedia.org/wiki/Monitor_(synchronization)">monitors</a>. In C#, the monitor implementation is <code>lock</code> statement. To apply it, we need 'locker object', which has to be locked before access to shared resources and unlocked after. Once 'locker object' is locked, other threads has to wait until it becomes unlocked. Look at below example (from Albahari's eBook):</p>
{% highlight csharp %}
using System;
using System.Threading;
class ThreadTest
{
  static bool done;    // Static fields are shared between all threads
  static void Main()
  {
    new Thread (Go).Start();
    Go();
  }
  static void Go()
  {
    if (!done) { done = true; Console.WriteLine (&quot;Done&quot;); }
  }
}
{% endhighlight %}

<p>The <code>bool</code> variable <code>done</code> is shared resource. Above program will have 2 threads. First one, starts in a new thread and second one, right after the first one, in main thread. Both will try to access shared resource. We can see that during method <code>Go()</code> execution, the shared variable is accessed actually 2 times. First - to check its value, and second - to set it (if it was false). The problem is that thread #1 can access it first (when it is false), then give up processor for thread #2, which also will check the value (still false) and we will get "Done" printed twice. That's something we do not want. To solve this issue, we introduce 'locker object' represented by variable <code>locker</code>.

{% highlight csharp %}
using System;
using System.Threading;
class ThreadSafe
{
  static bool done;
  static readonly object locker = new object();
  static void Main()
  {
    new Thread (Go).Start();
    Go();
  }
  static void Go()
  {
    lock (locker)
    {
      if (!done) { Console.WriteLine (&quot;Done&quot;); done = true; }
    }
  }
}
{% endhighlight %}

<p>Now, the if statement is secured by lock. Every thread, which wants to enter it, has to obtain the lock. Once one thread obtain the lock, another threads cannot. They have to wait, until it becomes unlocked. In above example, when thread #1 has the lock and start executing critical section, then even if it give up for thread #2, we have warranty that another thread will not enter the critical section. Additionally, only thread #1 can release the lock.</p>
<p>The following code:</p>

{% highlight csharp %}
lock(locker)
{
    //code
}
{% endhighlight %}

<p>is equivalent to (C# 4.0):</p>

{% highlight csharp %}
bool lockTaken = false;
try
{
  Monitor.Enter (locker, ref lockTaken);
  //code
}
finally { if (lockTaken) Monitor.Exit (locker); }
{% endhighlight %}

<h3>Signaling</h3>
<p>Another common technique in multithreaded applications is signaling. It is notifying other thread(s). For example: thread #1 can start another thread (thread #2) and wait for signal from it (e.g. that it finished some operation). Thread #2 is performing the operation, while thread #1 is waiting. Once thread #2 finish operation, it notify (send signal) thread #1, which then can continue other computations.</p>
<p>In the example below, then main thread, create new thread to perform <code>Operation</code>. After that it performs some computation and when it is done, it waits for thread #2 to finish its operations. After main thread get notification from thread #2, it can proceed.</p>

{% highlight csharp %}
using System;
using System.Threading;
class BasicWaitHandle
{
  static EventWaitHandle _waitHandle = new AutoResetEvent (false);
  static void Main()
  {
    new Thread (Operation).Start();
    Thread.Sleep (1000);                  // Computation...
    Console.WriteLine (&quot;Wait...&quot;);
    _waitHandle.WaitOne();                    // Wait for notification
    Console.WriteLine (&quot;Notified!&quot;);
  }
  static void Operation()
  {
    Console.WriteLine (&quot;Start operation...&quot;);
    Thread.Sleep(2000);               // Computation...
    Console.WriteLine (&quot;Operation finished!&quot;);
    _waitHandle.Set();                // Notify the Waiter
    Thread.Sleep(1000);         // Some other computation...
  }
}

{% endhighlight %}

<h3>Producer-Consumer</h3>
<p>The classic multithreaded application is <a href="http://en.wikipedia.org/wiki/Producer%E2%80%93consumer_problem">Producer–consumer</a>. Additionally, it is <a href="http://www.researchgate.net/post/In_which_area_of_Computer_Science_is_the_Producer_Consumer_Problem_applied_or_implemented">wide used across many real-life applications</a>. In the listing below, there is Producer-Consumer implementation in C# (taken from <a href="http://www.albahari.com/threading/part2.aspx#_WaitHandle_Producer_Consumer_Queue">Threading in C# - part 2</a>):</p>

{% highlight csharp %}
using System;
using System.Threading;
using System.Collections.Generic;
class ProducerConsumerQueue : IDisposable
{
  EventWaitHandle _wh = new AutoResetEvent (false);
  Thread _worker;
  readonly object _locker = new object();
  Queue<string> _tasks = new Queue<string>();
  public ProducerConsumerQueue()
  {
    _worker = new Thread (Work);
    _worker.Start();
  }
  public void EnqueueTask (string task)
  {
    lock (_locker) _tasks.Enqueue (task);
    _wh.Set();
  }
  public void Dispose()
  {
    EnqueueTask (null);     // Signal the consumer to exit.
    _worker.Join();         // Wait for the consumer's thread to finish.
    _wh.Close();            // Release any OS resources.
  }
  void Work()
  {
    while (true)
    {
      string task = null;
      lock (_locker)
        if (_tasks.Count > 0)
        {
          task = _tasks.Dequeue();
          if (task == null) return;
        }
      if (task != null)
      {
        Console.WriteLine (&quot;Performing task: &quot; + task);
        Thread.Sleep (1000);  // simulate work...
      }
      else
        _wh.WaitOne();         // No more tasks - wait for a signal
    }
  }
}
class Program
{
	static void Main()
	{
	  using (var q = new ProducerConsumerQueue())
	  {
	    q.EnqueueTask (&quot;Hello&quot;);
	    for (int i = 0; i < 10; i++) q.EnqueueTask (&quot;Say &quot; + i);
	    q.EnqueueTask (&quot;Goodbye!&quot;);
	  }
	  // Exiting the using statement calls q's Dispose method, which
	  // enqueues a null task and waits until the consumer finishes.
	}
}
{% endhighlight %}

<p>It takes advantage of locking and signaling. Producer is creating tasks and putting them into the buffer. Consumer is consuming tasks (fetching them from the buffer). In above program: the buffer is implemented as Queue. </p>
<p>There are two threads:</p>
<ul>
<li>Main thread - creating tasks and adding them into the queue (enqueuing)</li>
<li>Work thread - processing tasks (dequeuing)</li>
</ul>
<p>'Work thread' is consuming tasks if the queue is not empty. If the queue is empty, instead of checking its content continuously, it waits for the signal from Main thread. The Main thread notify Work thread every time it enqueued new task into the queue. Work thread terminates, once it receive <code>null</code> task. In above program, it happens when we quit the <code>using</code> statement in Main thread. That cause <code>Dispose()</code> method call (in <code>ProducerConsumerQueue</code> class), which enqueues <code>null</code> task into the queue. During enqueuing and dequeuing, the queue is locked using <code>lock</code> construct.</p>
<p>More detailed description of this implementation can be found on <a href="http://www.albahari.com/threading/part2.aspx#_WaitHandle_Producer_Consumer_Queue">Joe Albahari's article</a>.</p>
<h3>Summary</h3>
<p>There are many advantages of multithreading: speeding up applications by performing operations in different thread, while processor is waiting for I/O operation or making UI thread responsive all the time, while processing is done in background. However, multithreaded applications are much harder to find bugs and debug. Because of that: you should avoid multithreading everywhere when possible. Especially, when threads access the shared resource.</p>
<p>To get familiar with multithreading you can read <a href="http://www.devmanuals.com/tutorials/java/corejava/MultiThreading.html">Introduction to Multithreading</a> (with examples in Java) and <a href="http://www.yoda.arachsys.com/csharp/threads/">Multi-threading in .NET: Introduction and suggestions</a> (with "Hello, world" example in C#).</p>
<p>For a jump start you may find useful a session from TechEd New Zealand 2012: <a href="http://channel9.msdn.com/Events/TechEd/NewZealand/TechEd-New-Zealand-2012/DEV402">Multi-threaded Programming in .NET from the ground up</a> (it's 2 years old, but still accurate).</p>
<p><iframe style="height:270px;width:480px" src="http://channel9.msdn.com/Events/TechEd/NewZealand/TechEd-New-Zealand-2012/DEV402/player?w=480&amp;h=270" frameborder="0" scrolling="no"></iframe></p>
<p>To learn more about multithreading in C#, I strongly recommend you <a href="http://www.albahari.com/threading/">Threading in C#</a> by Joseph Albahari, which is also part of <a href="http://www.amazon.com/5-0-Nutshell-The-Definitive-Reference/dp/1449320104">C# 5.0 in a Nutshell</a> (book I am reading now...and also recommending!). </p>

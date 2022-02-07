---
layout: post
title: PyGTK, Multithreading and progress bar
date: 2013-08-20 10:17:46.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- developer
- multithreading
- pygtk
- python
meta:
  _edit_last: '1'
  _syntaxhighlighter_encoded: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  dsq_thread_id: '1620961317'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/pygtk-multithreading-and-progress-bar/"
---
<p>Multithreading in Python seems to be very simple. Let's look at the example:</p>

{% highlight python %}
import threading
import time
global_var = 0
class ThreadClass(threading.Thread):
	def run(self):
		global global_var
		while True:
			print global_var
class ThreadClass2(threading.Thread):
	def run(self):
		global global_var
		while True:
			time.sleep(1)
			global_var += 1
t1 = ThreadClass()
t1.start()
t2 = ThreadClass2()
t2.start()
t1.join()
t2.join()
{% endhighlight %}

<p>Thread 1 is printing the <em>global_var</em> and Thread 2 is incrementing it by 1, every second.</p>

<p>Recently I needed to use threads in PyGTK to display progress bar. Off course the state of progress bar was dependent on the other thread. It had to be updated after each subtask call. This is the code:</p>

{% highlight python %}
import threading
import time
import gtk
def init_progressbar():
    main_box = gtk.VBox()
    progressbar = gtk.ProgressBar()
    progressbar_box = gtk.HBox(False, 20)
    main_box.pack_start(progressbar_box, False, False, 20)
    progressbar_box.pack_start(progressbar)
    info_box = gtk.VBox()
    main_box.pack_start(info_box, False, False, 10)
    info_label = gtk.Label("Running...")
    info_box.pack_start(info_label)
    return main_box, progressbar, info_label
def run_tasks(pb, info_label):
    task_list = ['task1', 'task2', 'task3', 'task4']
    task_no = 0
    for task in task_list:
        pb.set_fraction(float(task_no)/len(task_list))
        run_task(2, task, info_label)
        task_no += 1
    pb.set_fraction(float(task_no)/len(task_list))
    info_label.set_text('Finished')
def run_task(delay, task, info_label):
    info_label.set_text(task + ' is running...')
    time.sleep(delay)   # simulation of running the task
win_pb, pb, info_label = init_progressbar()
win = gtk.Window()
win.set_default_size(400,100)
win.add(win_pb)
win.show_all()
win.connect("destroy", lambda _: gtk.main_quit())
t = threading.Thread(target=run_tasks, args=(pb,info_label))
t.start()
gtk.main()
{% endhighlight %}

<p>And...it was not working. The progress bar (and the label) did not get updated after task calls. Why?</p>
<p>It was caused by the fact, that PyGTK is not thread safe. Fortunately we have function <em>threads_init()</em> in <em>gobject</em> module, which can handle it. We just need to call <em>gobject.threads_init()</em> before first thread creation. Corrected (working) code looks like that:</p>

{% highlight python %}
import threading
import time
import gobject
import gtk
def init_progressbar():
    main_box = gtk.VBox()
    progressbar = gtk.ProgressBar()
    progressbar_box = gtk.HBox(False, 20)
    main_box.pack_start(progressbar_box, False, False, 20)
    progressbar_box.pack_start(progressbar)
    info_box = gtk.VBox()
    main_box.pack_start(info_box, False, False, 10)
    info_label = gtk.Label("Running...")
    info_box.pack_start(info_label)
    return main_box, progressbar, info_label
def run_tasks(pb, info_label):
    task_list = ['task1', 'task2', 'task3', 'task4']
    task_no = 0
    gobject.threads_init()
    for task in task_list:
        pb.set_fraction(float(task_no)/len(task_list))
        run_task(2, task, info_label)
        task_no += 1
    pb.set_fraction(float(task_no)/len(task_list))
    info_label.set_text('Finished')
def run_task(delay, task, info_label):
    info_label.set_text(task + ' is running...')
    time.sleep(delay)   # simulation of running the task
win_pb, pb, info_label = init_progressbar()
win = gtk.Window()
win.set_default_size(400,100)
win.add(win_pb)
win.show_all()
win.connect("destroy", lambda _: gtk.main_quit())
t = threading.Thread(target=run_tasks, args=(pb,info_label))
t.start()
gtk.main()
{% endhighlight %}

<p>I wanted also to be able to cancel program computation, by the cancel button. To do that I needed shared variable to be a status flag informing, whether computation should be cancelled or continued. It had to be accessible in task loop and cancel event. </p>
<p>In Python there are mutable and immutable objects. Mutable are passed by reference, but immutable - by value. More about that on <a href="http://stackoverflow.com/questions/986006/python-how-do-i-pass-a-variable-by-reference">this StackOverflow question</a>. Boolean type is immutable, but there is a way around this: use list (mutable type) with one element (boolean variable). I know it is awful solution, but I did not find any better. If you know one, let me know!</p>
<p>This is the app with cancel button:</p>

{% highlight python %}
import threading
import time
import gobject
import gtk
def init_progressbar():
    main_box = gtk.VBox()
    progressbar = gtk.ProgressBar()
    progressbar_box = gtk.HBox(False, 20)
    main_box.pack_start(progressbar_box, False, False, 20)
    progressbar_box.pack_start(progressbar)
    info_box = gtk.VBox()
    main_box.pack_start(info_box, False, False, 10)
    info_label = gtk.Label("Running...")
    info_box.pack_start(info_label)
    cancel_box = gtk.HBox()
    info_box.pack_start(cancel_box)
    cancel_button = gtk.Button("Cancel")
    cancel = [False]
    cancel_button.connect("clicked", cancel_counting, info_label, cancel)
    cancel_box.pack_start(cancel_button, False, False, 20)
    return main_box, progressbar, info_label, cancel
def run_tasks(pb, info_label, cancel):
    task_list = ['task1', 'task2', 'task3', 'task4']
    task_no = 0
    gobject.threads_init()
    for task in task_list:
        if cancel[0]:
            pb.set_fraction(0)
            info_label.set_text('Canceled')
            return
        pb.set_fraction(float(task_no)/len(task_list))
        run_task(2, task, info_label)
        task_no += 1
    pb.set_fraction(float(task_no)/len(task_list))
    info_label.set_text('Finished')
def run_task(delay, task, info_label):
    info_label.set_text(task + ' is running...')
    time.sleep(delay)   # simulation of running the task
def cancel_counting(widget, info_label, cancel):
    cancel[0] = True
    info_label.set_text("Cancelling...")
win_pb, pb, info_label, cancel = init_progressbar()
win = gtk.Window()
win.set_default_size(400,100)
win.add(win_pb)
win.show_all()
win.connect("destroy", lambda _: gtk.main_quit())
t = threading.Thread(target=run_tasks, args=(pb,info_label, cancel))
t.start()
gtk.main()
{% endhighlight %}

<p>To make above code working on your machine you need to have Python and PyGTK installed. To find out the details, how to install Python and/or PyGTK check my <a href="http://jj09.net/python-jump-start/">Python jump start</a> post.</p>

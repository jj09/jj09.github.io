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
<p>[python]import threading<br />
import time</p>
<p>global_var = 0</p>
<p>class ThreadClass(threading.Thread):<br />
	def run(self):<br />
		global global_var<br />
		while True:<br />
			print global_var</p>
<p>class ThreadClass2(threading.Thread):<br />
	def run(self):<br />
		global global_var<br />
		while True:<br />
			time.sleep(1)<br />
			global_var += 1</p>
<p>t1 = ThreadClass()<br />
t1.start()</p>
<p>t2 = ThreadClass2()<br />
t2.start()</p>
<p>t1.join()<br />
t2.join()[/python]</p>
<p>Thread 1 is printing the <em>global_var</em> and Thread 2 is incrementing it by 1, every second.</p>
<p>Recently I needed to use threads in PyGTK to display progress bar. Off course the state of progress bar was dependent on the other thread. It had to be updated after each subtask call. This is the code:</p>
<p>[python]import threading<br />
import time<br />
import gtk</p>
<p>def init_progressbar():<br />
    main_box = gtk.VBox()<br />
    progressbar = gtk.ProgressBar()<br />
    progressbar_box = gtk.HBox(False, 20)<br />
    main_box.pack_start(progressbar_box, False, False, 20)<br />
    progressbar_box.pack_start(progressbar)<br />
    info_box = gtk.VBox()<br />
    main_box.pack_start(info_box, False, False, 10)<br />
    info_label = gtk.Label(&quot;Running...&quot;)<br />
    info_box.pack_start(info_label)<br />
    return main_box, progressbar, info_label</p>
<p>def run_tasks(pb, info_label):<br />
    task_list = ['task1', 'task2', 'task3', 'task4']<br />
    task_no = 0<br />
    for task in task_list:<br />
        pb.set_fraction(float(task_no)/len(task_list))<br />
        run_task(2, task, info_label)<br />
        task_no += 1<br />
    pb.set_fraction(float(task_no)/len(task_list))<br />
    info_label.set_text('Finished')</p>
<p>def run_task(delay, task, info_label):<br />
    info_label.set_text(task + ' is running...')<br />
    time.sleep(delay)   # simulation of running the task</p>
<p>win_pb, pb, info_label = init_progressbar()<br />
win = gtk.Window()<br />
win.set_default_size(400,100)<br />
win.add(win_pb)<br />
win.show_all()<br />
win.connect(&quot;destroy&quot;, lambda _: gtk.main_quit())<br />
t = threading.Thread(target=run_tasks, args=(pb,info_label))<br />
t.start()<br />
gtk.main()<br />
[/python]</p>
<p>And...it was not working. The progress bar (and the label) did not get updated after task calls. Why?</p>
<p>It was caused by the fact, that PyGTK is not thread safe. Fortunately we have function <em>threads_init()</em> in <em>gobject</em> module, which can handle it. We just need to call <em>gobject.threads_init()</em> before first thread creation. Corrected (working) code looks like that:</p>
<p>[python]import threading<br />
import time<br />
import gobject<br />
import gtk</p>
<p>def init_progressbar():<br />
    main_box = gtk.VBox()<br />
    progressbar = gtk.ProgressBar()<br />
    progressbar_box = gtk.HBox(False, 20)<br />
    main_box.pack_start(progressbar_box, False, False, 20)<br />
    progressbar_box.pack_start(progressbar)<br />
    info_box = gtk.VBox()<br />
    main_box.pack_start(info_box, False, False, 10)<br />
    info_label = gtk.Label(&quot;Running...&quot;)<br />
    info_box.pack_start(info_label)<br />
    return main_box, progressbar, info_label</p>
<p>def run_tasks(pb, info_label):<br />
    task_list = ['task1', 'task2', 'task3', 'task4']<br />
    task_no = 0<br />
    gobject.threads_init()<br />
    for task in task_list:<br />
        pb.set_fraction(float(task_no)/len(task_list))<br />
        run_task(2, task, info_label)<br />
        task_no += 1<br />
    pb.set_fraction(float(task_no)/len(task_list))<br />
    info_label.set_text('Finished')</p>
<p>def run_task(delay, task, info_label):<br />
    info_label.set_text(task + ' is running...')<br />
    time.sleep(delay)   # simulation of running the task</p>
<p>win_pb, pb, info_label = init_progressbar()<br />
win = gtk.Window()<br />
win.set_default_size(400,100)<br />
win.add(win_pb)<br />
win.show_all()<br />
win.connect(&quot;destroy&quot;, lambda _: gtk.main_quit())<br />
t = threading.Thread(target=run_tasks, args=(pb,info_label))<br />
t.start()<br />
gtk.main()<br />
[/python]</p>
<p>I wanted also to be able to cancel program computation, by the cancel button. To do that I needed shared variable to be a status flag informing, whether computation should be cancelled or continued. It had to be accessible in task loop and cancel event. </p>
<p>In Python there are mutable and immutable objects. Mutable are passed by reference, but immutable - by value. More about that on <a href="http://stackoverflow.com/questions/986006/python-how-do-i-pass-a-variable-by-reference">this StackOverflow question</a>. Boolean type is immutable, but there is a way around this: use list (mutable type) with one element (boolean variable). I know it is awful solution, but I did not find any better. If you know one, let me know!</p>
<p>This is the app with cancel button:</p>
<p>[python]import threading<br />
import time<br />
import gobject<br />
import gtk</p>
<p>def init_progressbar():<br />
    main_box = gtk.VBox()<br />
    progressbar = gtk.ProgressBar()<br />
    progressbar_box = gtk.HBox(False, 20)<br />
    main_box.pack_start(progressbar_box, False, False, 20)<br />
    progressbar_box.pack_start(progressbar)<br />
    info_box = gtk.VBox()<br />
    main_box.pack_start(info_box, False, False, 10)<br />
    info_label = gtk.Label(&quot;Running...&quot;)<br />
    info_box.pack_start(info_label)<br />
    cancel_box = gtk.HBox()<br />
    info_box.pack_start(cancel_box)<br />
    cancel_button = gtk.Button(&quot;Cancel&quot;)<br />
    cancel = [False]<br />
    cancel_button.connect(&quot;clicked&quot;, cancel_counting, info_label, cancel)<br />
    cancel_box.pack_start(cancel_button, False, False, 20)<br />
    return main_box, progressbar, info_label, cancel</p>
<p>def run_tasks(pb, info_label, cancel):<br />
    task_list = ['task1', 'task2', 'task3', 'task4']<br />
    task_no = 0<br />
    gobject.threads_init()<br />
    for task in task_list:<br />
        if cancel[0]:<br />
            pb.set_fraction(0)<br />
            info_label.set_text('Canceled')<br />
            return<br />
        pb.set_fraction(float(task_no)/len(task_list))<br />
        run_task(2, task, info_label)<br />
        task_no += 1<br />
    pb.set_fraction(float(task_no)/len(task_list))<br />
    info_label.set_text('Finished')</p>
<p>def run_task(delay, task, info_label):<br />
    info_label.set_text(task + ' is running...')<br />
    time.sleep(delay)   # simulation of running the task</p>
<p>def cancel_counting(widget, info_label, cancel):<br />
    cancel[0] = True<br />
    info_label.set_text(&quot;Cancelling...&quot;)</p>
<p>win_pb, pb, info_label, cancel = init_progressbar()<br />
win = gtk.Window()<br />
win.set_default_size(400,100)<br />
win.add(win_pb)<br />
win.show_all()<br />
win.connect(&quot;destroy&quot;, lambda _: gtk.main_quit())<br />
t = threading.Thread(target=run_tasks, args=(pb,info_label, cancel))<br />
t.start()<br />
gtk.main()<br />
[/python]</p>
<p>To make above code working on your machine you need to have Python and PyGTK installed. To find out the details, how to install Python and/or PyGTK check my <a href="http://jj09.net/python-jump-start/">Python jump start</a> post.</p>
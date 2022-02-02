---
layout: post
title: Testing focus in JavaScript
date: 2016-01-28 22:01:32.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- javascript
- keyboard
- unit tests
meta:
  _edit_last: '1'
  _oembed_436483db4f15bb3e88b9ba2fcf68e482: "{{unknown}}"
  layout: default
  feature_size: blank
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  builder_switch_frontend: '0'
  dsq_thread_id: '4532824437'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/testing-focus-in-javascript/"
---
<p>This blog post is an overview of testing focus behavior in web browser.</p>
<p>During the work on Azure Portal I spent quite a bit of time on ensuring rich keyboard support. This requires appropriate focus management. When user press some keyboard shortcut, the focus should move to appropriate element. There is a good article on MDN about <a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/Keyboard-navigable_JavaScript_widgets">Keyboard-navigable JavaScript widgets</a>. Focus behavior should be also tested very succinctly. As it is very easy to change (break) with even the smallest change in the HTML or JavaScript.</p>
<p>Standard test goes as follows:</p>
<ul>
<li>Arrange: open some page</li>
<li>Act: execute some keyboard shortcut that should open particular page and/or set focus on particular element</li>
<li>Assert: check if expected element is focused</li>
</ul>
<h3>How to check if element is focused</h3>
<p>The simplest way is to use jQuery:</p>

{% highlight javascript %}
expect($(element).is(':focus')).equals(true);
{% endhighlight %}

<p>However this may not always work. Especially if you run your unit tests in parallel, because <a href="https://shanetomlinson.com/2014/test-element-focus-javascript/"><em>$element.is(':focus')</em> will not work when window does not have focus</a>.</p>
<p>The better (right) way is to use <em>document.activeElement</em>:</p>

{% highlight javascript %}
expect(document.activeElement).equals(element);
{% endhighlight %}

<p>This will work even when browser window is not focused.</p>
<h3>Testing async actions</h3>
<p>Sometimes, keyboard invoke asynchronous actions that eventually will change focus. This can cause:</p>
<ul>
<li>false negative tests: assertion was executed before focus was eventually set</li>
<li>false positives: finally focused element, got focus after assertion was executed</li>
</ul>
<p>The simplest recipe for the first problem is to delay assertion:</p>

{% highlight javascript %}
setTimeout(() => {
    expect(document.activeElement).equals(element);
    done();
}, 100);

{% endhighlight %}

<p>The problem with this approach is choosing appropriate delay for assertion. Therefore it is better to avoid raw <em>setTimeout</em>, and use polling approach that I described in my post <a href="http://jj09.net/settimeout-considered-harmful/">setTimeout considered harmful</a>:</p>

{% highlight javascript %}
poll(
  () => document.activeElement === element, 
  () => {
        assert(true);
        start();
  },
  () => {
        assert(false);
        start();
  }
);

{% endhighlight %}

<p>The polling function can be also used for the second solution (by changing assertion order in callback functions). However, for the false positives problem, simple <em>setTimeout</em> is good enough, because we do not have a choice other than wait some particular period of time to execute assertion.</p>
<h3>Invoking keyboard actions</h3>
<p>There are 3 types of events that we can use to simulate keyboard action:</p>
<ul>
<li><em>keydown</em></li>
<li><em>keyup</em></li>
<li><em>keypress</em></li>
</ul>
<p>The safest bet is to use <em>keydown</em>. Why? An example might be using special keys. While in case of <em>keypress</em> - various browsers handle it differently (e.g., by not triggering the event), <em>keydown</em> is pretty consistent. I recommend you to check <a href="http://unixpapa.com/js/key.html">this article</a> if you are interested in details. It was not updated for some time, but it will give you an idea.</p>
<p>In order to detect keyboard actions you may handle events on <a href="http://javascript.info/tutorial/bubbling-and-capturing">capture or bubbling phase</a>. You should choose model depending on your needs, but in general bubbling phase is optimal solution. Additionally it is supported by jQuery, with browser inconsistencies taken care of for you.</p>
<p>To invoke <em>keydown</em> event in your tests, you need to set focus on the element first:</p>

{% highlight javascript %}
$(element)
  .focus()
  .trigger("keydown", { which: keyCode });

{% endhighlight %}

<p>You can find JavaScript key codes <a href="https://css-tricks.com/snippets/javascript/javascript-keycodes/">here</a>.</p>
<h3>Summary</h3>
<p>Use <em>document.activeElement</em> to check which element is focused.<br />
Use polling approach for testing async actions.<br />
Use <em>keydown</em> event, and bubble phase to invoke/handle keyboard actions.</p>

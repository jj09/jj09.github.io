---
layout: post
title: setTimeout considered harmful
date: 2015-08-03 20:30:15.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- javascript
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
  builder_switch_frontend: '0'
  dsq_thread_id: '4000944578'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/settimeout-considered-harmful/"
---
<p><img class="aligncenter size-full wp-image-10311" src="{{ site.baseurl }}/assets/2015/08/setTimeout-SteveTweet.png" alt="setTimeout - Steve's Tweet" width="603" height="269" /></p>
<p>Recently I learned the hard way about setTimeouts side effects.</p>
<h3>101 setTimeout issue</h3>
<p>Let's say we have a following piece of code:</p>
{% highlight javascript %}
var someVar = 0;

var changeVar = function () {
    someVar = 10;
};
{% endhighlight %}
<p>And unit test:</p>
{% highlight javascript %}
QUnit.asyncTest('should change variable to 10', function () {
    // Arrange
    someVar = 0;

    // Act
    changeVar();

    // Assert
    equals(someVar, 10);
});
{% endhighlight %}
<p>Of course test passes, and we are happy.</p>
<p>Then, after some time, because of a reason (e.g., we want to fix some bug), we are adding <em>setTimeout</em> to <em>changeVar</em> function:</p>
{% highlight javascript %}
var changeVar = function () {
    setTimeout(function () {
        someVar = 10;
    }, 10);
};
{% endhighlight %}
<p>Unit test does not pass anymore. So we are adding <em>setTimeout</em> to our unit test as well (ideally: appropriately longer than one in <em>changeVar</em> function to avoid confusion!):</p>
{% highlight javascript %}
QUnit.asyncTest('should change variable to 10', function () {
    // Arrange
    someVar = 0;

    // Act
    changeVar();

    // Assert
    setTimeout(function () {
        equals(someVar, 10);
    }, 20);
});
{% endhighlight %}
<p>Then, we are introducing change to our code. Update only when <em>someVar</em> is not zero. We update function, and test accordingly:</p>
{% highlight javascript %}
var changeVar = function () {
    setTimeout(function () {
        if (someVar !== 0) {
            someVar = 10;
        }
    }, 10);
};

QUnit.asyncTest('should change variable to 10 if someVar != 0', function () {
    // Arrange
    someVar = 0;

    // Act
    changeVar();

    // Assert
    setTimeout(function () {
        equal(someVar, 0);
    }, 20);
});
{% endhighlight %}
<p>Everything works. Great! Then, somebody else is fixing another bug - of course by increasing timeout:</p>
{% highlight javascript %}
var changeVar = function () {
    setTimeout(function () {
        if (someVar !== 0) {
            someVar = 10;
        }
    }, 50);
};
{% endhighlight %}
<p>Still works, but when after some time we decide to change our logic:</p>
{% highlight javascript %}
var changeVar = function () {
    setTimeout(function () {
        if (someVar === 0) {
            someVar = 10;
        }
    }, 50);
};
{% endhighlight %}
<p>Our test is still passing...when it shouldn't!</p>
<p>Of course all of this is happening in large codebase with more complex logic.</p>
<p>But this is not that bad. Let's take a look at more interesting scenario.</p>
<h3>More complex case</h3>
<p>We are in worst situation when we have waterfall of <em>setTimeout</em>s.</p>
{% highlight javascript %}
var fun1 = function () {
    setTimeout(function () {
        someVar++;
    }, 10);
};

var fun2 = function () {
    setTimeout(function () {
        fun1();
        someVar = 10;
    }, 10);
};
{% endhighlight %}
<p>Guess if this unit test will pass:</p>
{% highlight javascript %}
QUnit.asyncTest('should change variable to 11', function() {
    // Arrange
    someVar = 0;

    // Act
    fun2();

    // Assert
    setTimeout(function () {
    	equal(someVar, 11);
    	start();
    }, 20);
});
{% endhighlight %}
<p>You think it should? You are wrong!</p>
<p>But this test will pass:</p>
{% highlight javascript %}
QUnit.asyncTest('should change variable to 11', function() {
    // Arrange
    someVar = 0;

    // Act
    fun2();

    // Assert
    setTimeout(function () {
    	equal(someVar, 11);
    	start();
    }, 21);
});
{% endhighlight %}
<p>Do you see the difference? Yes, timeout is 21 instead of 20. And of course everything will fall apart if somebody increase timeout in <em>fun1</em> or <em>fun2</em>.</p>
<h3>Solution</h3>
<p>The best solution is not to use <em>setTimeout</em> at all. Unfortunately we need async operations sometimes. In this case - you should use promises if possible. Unfortunately World is not perfect, especially Web Development World, and sometimes you have to use <em>setTimeout</em> (e.g., for UI effects etc.). You may think that if you set long enough timeout in your unit tests, everything should be good, right? Well...remember that it will make your unit tests slower. Instead - you should use <a href="http://davidwalsh.name/javascript-polling">polling approach</a>.</p>
<p>To apply it to the last example - using "Without Deferreds" approach - copy poll function to your codebase:</p>
{% highlight javascript %}
function poll(fn, callback, errback, timeout, interval) {
    var endTime = Number(new Date()) + (timeout || 2000);
    interval = interval || 100;

    (function p() {
            // If the condition is met, we're done! 
            if(fn()) {
                callback();
            }
            // If the condition isn't met but the timeout hasn't elapsed, go again
            else if (Number(new Date()) < endTime) {
                setTimeout(p, interval);
            }
            // Didn't match and too much time, reject!
            else {
                errback(new Error('timed out for ' + fn + ': ' + arguments));
            }
    })();
}
{% endhighlight %}
<p>And call it in your unit test:</p>
{% highlight javascript %}
QUnit.asyncTest('should change variable to 11', function() {
    // Arrange
    someVar = 0;

    // Act
    fun2();

    // Assert
    poll(
	    function() {
	        return someVar === 11;
	    },
	    function() {
	        ok(true);
	        start();
	    },
	    function() {
	        ok(false);
	        start();
	    }
	);
});
{% endhighlight %}
<p>Now, you do not have to guess what value will be appropriate for <em>setTimeout</em> delay, and you will speed up your tests as well.</p>
<p>When I see some strange behavior in code, the first thing I am looking at are <em>setTimeout</em> calls.</p>

---
layout: post
title: Properly measuring HTTP request time with node.js
date: 2018-02-23 11:10:35.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- node
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
  dsq_thread_id: '6500181001'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/properly-measuring-http-request-time-with-node-js/"
---
<p>When your backend code is calling external APIs you may want to measure particular request time to identify bottlenecks.</p>
<p>The most straightforward, but incorrect, way to measure how long a request takes is to use JavaScript <code>Date</code> object:</p>

{% highlight javascript %}
var request = require('request');

let start_time = new Date().getTime();

request.get('https://google.com', function (err, response) {
    console.log('Time elapsed:', new Date().getTime() - start_time);
});
{% endhighlight %}

<p>However, this won't give you the actual time that request takes. The above request call is async, and you start measuring time at the time when the request was queued, not actually sent.</p>
<p>In order to determine how much time elapsed since sending the request, you can use the <code>time</code> parameter:</p>

{% highlight javascript %}
var request = require('request');

request.get({ url: 'http://www.google.com', time: true }, function (err, response) {
    console.log('The actual time elapsed:', response.elapsedTime);
});
{% endhighlight %}

<p>You can also compare results returned by both methods:</p>

{% highlight javascript %}
var request = require('request');

let start_time = new Date().getTime();

request.get('https://google.com', function (err, response) {
    console.log('Time elapsed since queuing the request:', new Date().getTime() - start_time);
});

request.get({ url: 'http://www.google.com', time: true }, function (err, response) {
    console.log('The actual time elapsed:', response.elapsedTime);
});
{% endhighlight %}

<p>When I run it, I got the following results:</p>
<p><code>The actual time elapsed: 72<br />
Time elapsed since queuing the request: 156</code></p>
<p>Notice that the first callback resolves after the second one(!)</p>
<p>The difference is almost 2x. Depending on your server-side code, this difference might be even larger, and give you incorrect hints while you are profiling your application.</p>

<h3>2023 Update</h3>

Since [request package](https://www.npmjs.com/package/request) is deprecated, you can use [superagent-node-http-timings](https://www.npmjs.com/package/superagent-node-http-timings) to get detailed http timings information:

{% highlight javascript %}
const superagent = require('superagent');
const logNetworkTime = require('superagent-node-http-timings');

superagent
  .get(`https://google.com`)
  .use(logNetworkTime((err, result) => {
    console.log(result);
  }))
  .then(x => x);
{% endhighlight %}

Sample result:

{% highlight json %}
{
  url: 'https://www.google.com/',
  status: 200,
  timings: {
    socketAssigned: 0.659234,
    dnsLookup: 5.110974,
    tcpConnection: 10.424859,
    tlsHandshake: 22.362443,
    firstByte: 66.831464,
    contentTransfer: 14.258803,
    total: 119.647777
  }
}
{% endhighlight %}

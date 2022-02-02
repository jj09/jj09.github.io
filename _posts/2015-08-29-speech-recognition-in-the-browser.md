---
layout: post
title: Speech Recognition in the Browser
date: 2015-08-29 23:45:00.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- javascript
- voice recognition
- Web Speech API
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
  dsq_thread_id: '4080072075'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/speech-recognition-in-the-browser/"
---
<p>Last Thursday I had a pleasure to give talk about Speech Recognition in the Browser at the <a href="http://www.codefellows.org/">Code Fellows</a> in Seattle.</p>

<p><script class="speakerdeck-embed" src="//speakerdeck.com/assets/embed.js" async="" data-id="aa2459863d4244f68222792860923a31" data-ratio="1.77777777777778"></script></p>

<p>Many people were surprised how easy it is to add speech recognition to your website with pure JavaScript. So I thought I will share a few code snippets here. It works in Chrome only so far.</p>

<h3>Recognizing speech</h3>

<p>This is how you can translate speech to text:</p>
{% highlight javascript %}
var sr = new webkitSpeechRecognition();
sr.onresult = function (evt) {
    console.log(evt.results[0][0].transcript);
};
sr.start();
{% endhighlight %}

<p>You can also get the confidence level of the result:</p>
{% highlight javascript %}
var sr = new webkitSpeechRecognition();
sr.onresult = function (evt) {
    console.log(evt.results[0][0].transcript, evt.results[0][0].confidence);
};
sr.start();
{% endhighlight %}

<p>You can get interim results:</p>
{% highlight javascript %}
sr.interimResults = true;	// false by default
sr.onresult = function(evt) {
	for (var i = 0; i < evt.results.length; ++i) {
		console.log(evt.results[i][0].transcript);
	};
};
{% endhighlight %}

<p>Or different alternatives of recognized speech:</p>
{% highlight javascript %}
sr.maxAlternatives = 10;	// default = 1
sr.onresult = function(evt) {
	for (var i = 0; i < evt.results[0].length; ++i) {
		console.log(evt.results[0][i].transcript);
	}
};
{% endhighlight %}

<p>You can set a language, e.g., to Polish:</p>
{% highlight javascript %}
sr.lang = 'pl-PL';
{% endhighlight %}

<p>All above will stop recognition when you stop speaking. In order to do not stop recognition you need to set <em>continuous</em> flag to <em>true</em>. Additionally, this will treat every fragment of you speech as interim result, so you need to update <em>onresult</em> callback too:</p>
{% highlight javascript %}
sr.continuous = true;	// false by default
sr.onresult = function(evt) {
	console.log(evt.results[evt.results.length-1][0].transcript);
};
{% endhighlight %}

<p>Speech Recognition object has other callbacks (than <em>onresult</em>) that you can take advantage of:</p>
{% highlight javascript %}
sr.onstart = function() { console.log("onstart"); };
sr.onend = function() { console.log("onend"); };
sr.onspeechstart = function() { console.info("speech start"); };
sr.onspeechend = function() { console.info("speech end"); };
{% endhighlight %}

<h3>Emitting speech</h3>
{% highlight javascript %}
var msg = new SpeechSynthesisUtterance('Hi, I\'m Jakub!');
speechSynthesis.speak(msg);
{% endhighlight %}

<p>You can also change the speaker voice:</p>
{% highlight javascript %}
var voices = window.speechSynthesis.getVoices();
msg.voice = voices[10]; // Note: some voices don't support altering params
{% endhighlight %}

<p>There is also other options you can set:</p>
{% highlight javascript %}
msg.volume = 1; // 0 to 1
msg.pitch = 2; //0 to 2
msg.text = 'Hello World';
msg.lang = 'en-US';

msg.onend = function(e) {
	console.log('Finished in ' + event.elapsedTime + ' seconds.');
};
{% endhighlight %}

<h3>Summary</h3>

<p>Speech is coming to the browser, and you can not stop it. The question is when most of websites will add voice support. Check out <a href="https://github.com/jj09/voiceCmdr">voiceCmdr</a> - a library that I <a href="http://jj09.net/voicecmdr-voice-commands-in-the-browser/">blogged about earlier this year</a>, which helps to add voice commands to your websites in very easy way. You can also check out <a href="http://bookslib.azurewebsites.net/">website</a> that can be navigated with voice commands - you can find available commands in my <a href="http://jj09.net/website-with-speech-recognition-for-free/">blog post</a>. You can find entire logic for voice commands support in <a href="https://bookslib.azurewebsites.net/app/app.js">this file</a> (lines: 38-103).</p>

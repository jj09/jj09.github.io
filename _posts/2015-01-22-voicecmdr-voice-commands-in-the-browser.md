---
layout: post
title: voiceCmdr - voice commands in the Browser
date: 2015-01-22 22:13:35.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- javascript
- Open Source
- voice recognition
meta:
  _edit_last: '1'
  _syntaxhighlighter_encoded: '1'
  layout: default
  feature_size: blank
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  builder_switch_frontend: '0'
  dsq_thread_id: '3447483028'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/voicecmdr-voice-commands-in-the-browser/"
---
<p><img class="aligncenter size-full wp-image-8011" src="{{ site.baseurl }}/assets/2015/01/voicerecognition.png" alt="voice recognition" width="398" height="306" /></p>
<p>Recently I discovered <a href="https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html">Web Speech API</a>. I was already talking to the browser using Google Hangout and Google Translator, but I have never thought about adding voice support to my own website.</p>
<p>I did some research, and I found a <a href="http://www.google.com/intl/en/chrome/demos/speech.html">demo</a>. Based on that I put up <a href="https://nancyonazure.azurewebsites.net/">simple demo website</a> (say: "show website blog", and it will take you directly to the sub page that can be also approached with 3 mouse clicks). For now speech recognition <a href="http://caniuse.com/#feat=web-speech">works only in Google Chrome and Safari</a>. In Chrome it is not SpeechRecognition API, but <strong>webkit</strong>SpeechRegognition API. I hope, in the near future, other browsers will also implement it. Especially Spartan, which is integrated with Cortana.</p>
<p>I noticed that while the API is flexible, it is not easy to use. I think, for most common scenarios, developer would like to be able to add commands associated with function callbacks, and control recognition state with start/stop actions.</p>
<p>I created a JavaScript library <a href="https://github.com/jj09/voiceCmdr">voiceCmdr</a>. It is a single .js file without any dependencies. You can install it with npm or bower (check <a href="https://github.com/jj09/voiceCmdr">README on github</a>).</p>
<p>You can add commands:</p>
{% highlight javascript %}
voiceCmdr.addCommand("go home", function () {
  // go to home page
});
{% endhighlight %}
<p>Callback function can have parameter, which is everything you said after command. E.g.:</p>
{% highlight javascript %}
voiceCmdr.addCommand("search", function (param) {
  // search for phrase specified in param
});
{% endhighlight %}
<p>You can also remove commands:</p>
{% highlight javascript %}
voiceCmdr.removeCommand("go home");
{% endhighlight %}
<p>In order to start listening for commands:</p>
{% highlight javascript %}
voiceCmdr.start();
{% endhighlight %}
<p>To stop listening:</p>
{% highlight javascript %}
voiceCmdr.stop();
{% endhighlight %}
<p>You can also invoke listening for single command:</p>
{% highlight javascript %}
voiceCmdr.getCommand();
{% endhighlight %}
<p>Check <a href="https://github.com/jj09/voiceCmdr/tree/master/examples">examples</a>, and be aware that Web Speech API works only through http, and https (<span style="text-decoration: underline;">it will not work if you open static html file</span>). The easiest way to run server is to use python SimpleHTTPServer:</p>
{% highlight javascript %}
python -m SimpleHTTPServer 8080
{% endhighlight %}
<p>This can also go another way (by browser talking to you) with <a href="http://updates.html5rocks.com/2014/01/Web-apps-that-talk---Introduction-to-the-Speech-Synthesis-API">Web Synthesis API</a>.</p>
<p>I am curious what do you think. Are we ready for voice commands in the browser? Are you concerned about your privacy (<a href="https://twitter.com/shanselman/status/558154885787430913">check Scott Hanselman's tweet</a>)?</p>

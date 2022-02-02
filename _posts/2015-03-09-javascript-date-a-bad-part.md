---
layout: post
title: 'JavaScript Date: a Bad Part'
date: 2015-03-09 20:29:49.000000000 -07:00
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
  _oembed_27d0cabf3f3404dee76811ee8ca61a3d: "{{unknown}}"
  _oembed_013666b3227e5b191407abf1054601d5: "{{unknown}}"
  builder_switch_frontend: '0'
  dsq_thread_id: '3582226665'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/javascript-date-a-bad-part/"
---
<p>We all know that JavaScript has some bad parts. However, one of them is usually forgotten, and skipped in most of "JavaScript Bad Parts" lists on the Internet. It is a <code>Date</code> object. You can have hard time working with it, especially if you want to support time zones. In this post I would like to outline quircks of <code>Date</code> in JavaScript.</p>
<h3>Basics</h3>
<p>In order to create a <code>Date</code> object, you just do:</p>
{% highlight javascript %}
var now = new Date();
{% endhighlight %}
<p>This will create a date set to now.<br />
If you want to create <code>Date</code> on specific day:</p>
{% highlight javascript %}
var year = 2015;
var month = 2-1; // February
var day = 27;
var now = new Date(year, month, day);
{% endhighlight %}
<p>Here you encounter the first quirk: months are numbered from 0 to 11. January is 0, December is 11.</p>
<p>You can also specify hours, minutes, seconds, and milliseconds as additional parameters (no more pitfalls here):</p>
{% highlight javascript %}
var year = 2015;
var month = 2-1; // February
var day = 27;
var hours = 14; // 2PM
var minutes = 56;
var seconds = 37;
var milliseconds = 997;
var now = new Date(year, month, day, hours, minutes, seconds, milliseconds);
{% endhighlight %}
<p>For more details about creating <code>Date</code>, check <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date">Date at MDN</a>.</p>
<h3>Formatting</h3>
<p>If you want to display a date, there are a few available converters. Here are the most commonly used:</p>
{% highlight javascript %}
var date = new Date(2015, 1, 27, 14, 56, 37, 997);
console.log(date.toDateString());       // Fri Feb 27 2015
console.log(date.toTimeString());       // 14:56:37 GMT-0800 (Pacific Standard Time)
console.log(date.toLocaleDateString()); // 2/27/2015
console.log(date.toLocaleTimeString()); // 2:56:37 PM
console.log(date.toUTCString());        // Fri, 27 Feb 2015 22:56:37 GMT
console.log(date.toGMTString());        // Fri, 27 Feb 2015 22:56:37 GMT
console.log(date.toISOString());        // 2015-02-27T22:56:37.997Z
console.log(date.toJSON());             // 2015-02-27T22:56:37.997Z
{% endhighlight %}
<p>Be careful with 3 and 4. Both return different results, depended on user's machine settings and geographical location. This may cause UI issues (some date formats might be long).</p>
<p>Converters 5 and 6 are equivalent in all, most popular browsers. However <code>toGMTString</code> is deprecated.</p>
<p>Converters 7 and 8 are also equivalent. Moreover, <code>toJSON</code> use <code>toISOString</code> underneath to return result.</p>
<p>There is no significant issues with displaying Date, but there is no way to format it with custom format (e.g., 'YYYY-MM-DD HH:mm') like in C# or Java.</p>
<p>Alternative for formatting is <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat">Intl.DateTimeFormat</a> object from <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl">ECMAScript Internationalization API</a>. However, this API is not yet supported by older browsers, most of mobile browsers, and Safari (check <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat#Browser_compatibility">browser compatibility on MDN</a>).</p>
<h3>Parsing</h3>
<p>More tricky than displaying dates, is parsing them. There are two common ways to parse date from string:</p>
{% highlight javascript %}
var parsedDate1 = new Date("2015-02-27 22:56:37");
var parsedDate2 = Date.parse("2015-02-27 22:56:37");
{% endhighlight %}
<p>First returns <code>Date</code> object, second - number 1425106597000 (milliseconds since January 1, 1970, 00:00:00 UTC).</p>
<p>There is one, very unpleasant detail in parsing:</p>
<blockquote><p>Given a date string of "March 7, 2014", parse() assumes a <strong>local time zone</strong>, but given an ISO format such as "2014-03-07" it will assume a <strong>time zone of UTC</strong>. Therefore Date objects produced using those strings will represent different moments in time unless the system is set with a local time zone of UTC. This means that two date strings that appear equivalent may result in two different values depending on the format of the string that is being converted (<strong>this behavior is changed in ECMAScript ed 6 so that both will be treated as local</strong>).</p>
<footer>Source: <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/parse">MDN</a></footer>
</blockquote>
<p>This means that <code>date1</code> and <code>date2</code> below (created from machine located in Seattle, WA) are different:</p>
{% highlight javascript %}
var date1 = new Date("2014-01-02");
var date2 = new Date("1/2/2014");
console.log(date1); // Wed Jan 01 2014 16:00:00 GMT-0800 (Pacific Standard Time)
console.log(date2); // Thu Jan 02 2014 00:00:00 GMT-0800 (Pacific Standard Time)
{% endhighlight %}
<p>Recommended format for parsing is: <code>YYYY/MM/DD</code> - user local settings independent. It always assumes local timezone offset for date string given as a parameter.</p>
{% highlight javascript %}
var date1 = new Date("2014/01/02");
console.log(date1); // Thu Jan 02 2014 00:00:00 GMT-0800 (Pacific Standard Time)
{% endhighlight %}
<h3>Timezones</h3>
<p>JavaScript <code>Date</code> object always assumes local timezone <span style="text-decoration: underline;">offset</span> for the machine on which it is displayed. What is important: JavaScript <code>Date</code> does not support time zones, but only timezone offsets. This is a definition of both <a href="http://en.wikipedia.org/wiki/Time_zone#Time_zones_and_time_offsets">from Wikipedia</a>:</p>
<blockquote><p>A <strong>time zone</strong> is a geographical region where just about everybody observes the same standard time.<br />
A <strong>time offset</strong> is an amount of time subtracted from or added to UTC to get the current civil time - whether it's standard time or Daylight saving time.</p></blockquote>
<p>In other words: time zone is constant (as long as government does not changed it) for some place (e.g., San Francisco) all the time, while time zone offset changes (usually, twice a year - this is what we call 'daylight savings').</p>
<p>To get timezone offset:</p>
{% highlight javascript %}
var myDate = new Date();
var timezoneOffset = myDate.getTimezoneOffset(); // result in minutes
{% endhighlight %}
<p>The result is in minutes. Here is another quirk: timezones that are 'west' from UTC (offset = 0) have positive values (60 - 720), and timezones that are 'east' from UTC have negative values (-60 - -780). Thus, Pacific Standard Time (UTC <strong>-8:00</strong>), in JavaScript, has timezone offset <strong>480</strong>, and Central European Time (UTC <strong>+1:00</strong>) has timezone offset <strong>-60</strong>.</p>
<p>One more pitfall: local timezone offset is always set depends on value of <code>Date</code> object. Thus, for Computer located in Seattle, WA:</p>
{% highlight javascript %}
var date1 = new Date(2015,1,20); // date in Pacific Standard Time (before timezone offset change)
var date2 = new Date(2015,2,20); // date in Pacific Daylight Time (after timezone offset change)
console.log(date1.getTimezoneOffset()); // 480
console.log(date2.getTimezoneOffset()); // 420
{% endhighlight %}
<p>In this case your current 'local' timezone offset (for the time in which you are creating Date object) does not matter.</p>
<p>Even if you create Date object with date before the time change, and then you modify it to date after the time change - its timezone offset changes to reflect offset for the new (current) value:</p>
{% highlight javascript %}
var date = new Date(2015,1,20); // date in Pacific Standard Time
console.log(date.getTimezoneOffset()); // 480
date.setMonth(2); // change month so date is in Pacific Daylight Time now
console.log(date.getTimezoneOffset()); // 420
{% endhighlight %}
<h3>Moment.js</h3>
<p><a href="http://momentjs.com/">Moment.js</a> is a JavaScript library designed to work on the client side (in browser), and on the server side (in node.js). It has a lot of functions to parse, display and manipulate dates. This makes dealing with dates less painful.</p>
<p><a href="http://momentjs.com/timezone/">Moment Timezone</a> - a library built on top of Moment.js - supports real time zones (not only timezone offsets). The data for Moment Timezone comes from <a href="http://www.iana.org/time-zones">the IANA Time Zone Database</a> - most popular time zone database. New versions are released periodically as timezone laws change in various countries.</p>
<p>Consider using Moment.js and Moment Timezone in your application when you are doing more complex operations with dates. Especially when you want to support time zones.</p>
<h3>Summary</h3>
<p>It is really surprising that working with dates in programming is still causing a lot of issues. However, we are getting better at that. To get a comprehensive overview of date/time in programming language I recommend <a href="http://www.pluralsight.com/courses/date-time-fundamentals">Date and Time Fundamentals</a> by <a href="http://codeofmatt.com/">Matt Johnson</a>. You can also check <a href="http://codeofmatt.com/">Matt Johnson's blog</a>. He blogs mainly about date/time in variety of environments. His article <a href="http://codeofmatt.com/2013/06/07/javascript-date-type-is-horribly-broken/">JavaScript Date type is horribly broken</a> might be good supplement for this post.</p>
<p>To get a quick insight why dealing with time zones is very complex, check <a href="https://www.youtube.com/watch?v=-5wpm-gesOY">this video</a>. It is also worth to check <a href="https://unix4lyfe.org/time/?v=1">What Every Programmer Should know about Time</a>.</p>

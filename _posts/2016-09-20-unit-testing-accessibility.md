---
layout: post
title: Unit Testing Accessibility
date: 2016-09-20 17:28:09.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- accessibility
- jasmine
- QUnit
- unit tests
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
  dsq_thread_id: '5160151414'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/unit-testing-accessibility/"
---
<p>In <a href="http://jj09.net/web-accessibility-hacker-way/">Web Accessibility Hacker Way</a> I mentioned that "only 20% of accessibility requirements can be verified by tools". Nevertheless, it is worth to cover this 20%. Especially, when it is not very hard. You know that having automated test that guard against regressions always pays off in a long run.</p>
<p>As of today the best automatic verification tool for accessibility is <a href="http://www.deque.com/products/axe/">aXe</a>.</p>
<p><img class="aligncenter size-full wp-image-15532" src="{{ site.baseurl }}/assets/2016/09/aXeLogo-300x300.png" alt="aXe" width="300" height="300" /></p>
<p>There is <a href="http://bitly.com/aXe-Chrome">aXe Chrome plugin</a> and <a href="http://bit.ly/aXe-Firefox">aXe Firefox plugin</a> that enables you to run accessibility audit manually:</p>
<p><img class="aligncenter size-full wp-image-15581" src="{{ site.baseurl }}/assets/2016/09/axe_results.jpg" alt="aXe - results" width="792" height="506" /></p>
<p>Running automated tool manually is useful, but it is better to run it automatically as unit test, and incorporate it into your Continuous Integration to run it automatically after every commit.</p>
<h3>Running accessibility audit with aXe</h3>
<p>You can install aXe with npm:</p>
<p><code>npm i axe-core</code></p>
<p>The aXe has a function <code>a11yCheck</code> that performs accessibility audit on specified HTML Element. You may run it against widgets or partial views on your web app. That function takes 2 parameters:</p>
<ol>
<li>HTMLElement to be audited</li>
<li>callback function that is invoked with <code>results</code> parameter</li>
</ol>

{% highlight javascript %}
axe.a11yCheck($("#myElement")[0], function (results) {
    expect(results.violations.length).toBe(0);
    results.violations.length && console.error(results.violations);
});
{% endhighlight %}

<p>It is useful to print errors to console, as the <code>results.violations</code> is an array of nested objects with different properties. Many of them are helpful to diagnose the issue.</p>
<p><img class="aligncenter size-full wp-image-15541" src="{{ site.baseurl }}/assets/2016/09/axe_consoleErrors.png" alt="aXe - console errors" width="790" height="366" /></p>
<p>*a11y is abbreviation for accessibility (similar like i18n for internationalization), 11 is number of letters between 'a' and 'y'</p>
<h3>Running aXe with Jasmine 2.x</h3>
<p>In order to run aXe with <a href="http://jasmine.github.io/">Jasmine</a>, you need to take into account that <code>a11yCheck</code> is asynchronous. Thus, you need to pass and invoke <code>done</code> function:</p>

{% highlight javascript %}
describe("a11y check", function() {
  it("has no accessbility violations (check console for errors)", function(done) {
    axe.a11yCheck($("#myElement")[0], function (results) {
        expect(results.violations.length).toBe(0);
        if (results.violations.length > 0) {
            console.error(results.violations);
        }
        done();
    });
  });
});
{% endhighlight %}

<h3>Running aXe with QUnit 2.x</h3>
<p>It is similar in <a href="https://qunitjs.com/">QUnit</a>. You also need to invoke <code>done</code> function, but first you need to get it by calling <code>assert.async()</code>:</p>

{% highlight javascript %}
QUnit.test("a11y check", function(assert) {
    var done = assert.async();

    axe.a11yCheck($("#myElement")[0], function (results) {
        assert.strictEqual(results.violations.length, 0, "There should be no A11y violations (check console for errors)");
        if (results.violations.length > 0) {
            console.error(results.violations);
        }
        done();
    });
});
{% endhighlight %}

<h3>Sample</h3>
<p>I created a sample with button and input tag:</p>

{% highlight html %}
<div id="fixture">
  <button>My button</button> 
  <input type="text" />
</div>
{% endhighlight %}

<p>This sample is not accessible because input tag does not have a label, and <code>a11yCheck</code> should report violations. The sample code, with Jasmine and QUnit tests, is available on github: <a href="https://github.com/jj09/axe-unittests">axe-unittests</a>.</p>
<h3>Summary</h3>
<p>While automated accessibility unit tests are great, you probably still want to use <a href="http://bitly.com/aXe-Chrome">aXe plugin for Chrome</a> to investigate reported violations. It's more convenient, and it has neat user interface, while in unit tests you need to dig in into console errors.</p>
<p>When you start adding accessibility checks for different parts of your system, you may encounter many violations at first. It is better to still add tests, that ignore known violations, and then incrementally fix the issues. This approach prevents regressions, while delaying adding test until all violations are fixed may cause introducing new ones while fixing others.</p>

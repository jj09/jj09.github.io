---
layout: post
title: Web Accessibility Hacker Way
date: 2016-08-22 22:31:33.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- accessibility
- html5
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
  dsq_thread_id: '5087561263'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/web-accessibility-hacker-way/"
---
<p><img class="aligncenter size-full wp-image-15121" src="{{ site.baseurl }}/assets/2016/08/Web_Accessibility_Meme.jpeg" alt="web accessibility meme" width="800" height="500" /></p>
<p>Have you heard about accessibility? Do you know what that is? Do you know what it takes to make your website accessible?</p>
<p>Making your website accessible means providing the ability for everyone - regardless of disability or special needs - to use it.</p>
<p>Unfortunately, if you put together all accessibility specifications and print it, the stack will be higher than CN Tower in Toronto:</p>
<p><img class="aligncenter size-full wp-image-15101" src="{{ site.baseurl }}/assets/2016/08/accessibility_cntower.jpg" alt="CN Tower (Toronto)" width="800" height="525" /></p>
<p>This is not very encouraging. Many people think that it is not worth the effort because the customer base with special needs is significantly low. However, there is a thing called <a href="http://accessibility.co.uk/wiki/situational-disability">situational disability</a> that applies to all of us. Moreover, when we are building our websites with accessibility in mind, we make them better for everyone. Why? Because everybody is more comfortable when allowed to fill out forms on a website using just a keyboard (without mouse) and able to switch between fields fast. Generally, everybody likes it when the focus is set on the search bar for sites because 99% of the time, the first thing you do is search for something. Everybody likes properly matched colors (accessible contrast).</p>
<p>How do you get started? How to survive without reading tons of specifications?</p>
<h3>3 steps to fulfill 80% standards with 20% effort</h3>
<ol>
<li><strong>Make your website <a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/Keyboard-navigable_JavaScript_widgets">usable with keyboard</a> only:</strong>
<ul>
<li>make sure that focus outline is visible all the time and user can determine which element is currently focused</li>
<li>no extra/unnecessary TAB stops</li>
<li>no tabstop traps (when you cannot get out of an element with the keyboard)</li>
</ul>
</li>
<li><strong>Implement smart focus management:</strong>
<ul>
<li>set focus on appropriate elements after user actions (e.g., when a user navigates to a page with a login form – set the focus on the login text field; in 90% of the cases the next user action will be entering the login)</li>
<li>restore focus to appropriate elements after user actions (e.g., when a user closes a menu, focus should be restored to the element that was focused on before opening the menu)</li>
<li>make tab order user-friendly (remove non-actionable and non-informative tab stops)</li>
</ul>
</li>
<li><strong>Make your website <a href="http://webaim.org/techniques/screenreader/">usable with screen reader</a>:</strong>
<ul>
<li>When element gets focused, screen reader should provide meaningful information to the user (e.g., "image Satya Nadella" when focused on Satya's image, or "menu collapsed" when focused on dropdown menu)</li>
<li>Min bar: make it good enough with one screen reader and one browser first. As of 2016-08-22 the best browser + screen reader combination is Firefox + <a href="http://webaim.org/articles/nvda/">NVDA</a> (it has a text mode that prints output instead of converting it into speech: Tools -&gt; Speech viewer)</li>
<li>Add aria tags to elements only when the screen reader cannot infer information from HTML (e.g., button element does not need role='button' as screen reader will infer it)</li>
</ul>
</li>
</ol>
<h3>Good to know</h3>
<ol>
<li>Don't focus too much on "being compliant to the standards" at the beginning. Just use the common sense and your intuition. You can deep dive into the standards later on.</li>
<li>Make your website's most common scenarios work well first and focus on less popular pages later.</li>
<li>Only 20% of accessibility requirements can be verified by tools. The rest has to be verified manually by:
<ul>
<li>yourself</li>
<li>user study</li>
<li>an accessibility expert</li>
</ul>
</li>
</ol>
<h3>Resources to get started</h3>
<ul>
<li><a href="https://teachaccess.github.io/tutorial/">Web Accessibility Tutorial</a>
<ul>
<li>Especially: <a href="https://teachaccess.github.io/tutorial/#/12">writing code checklist</a> and <a href="https://teachaccess.github.io/tutorial/#/19">design checklist</a></li>
</ul>
</li>
<li><a href="http://marcysutton.com/web-accessibility-resources/">Web Accessibility Resources</a> by <a href="http://marcysutton.com/">Marcy Sutton</a>
<ul>
<li>Especially: <a href="https://a11ywins.tumblr.com/">examples of accessible websites</a></li>
</ul>
</li>
<li><a href="https://app.pluralsight.com/library/courses/web-accessibility-getting-started">Web Accessibility: Getting Started (Pluralsight)</a></li>
<li>Examples:
<ul>
<li><a href="http://heydonworks.com/practical_aria_examples/">ARIA examples</a></li>
<li><a href="http://oaa-accessibility.org/">Open AJAX Accessibility examples</a></li>
</ul>
</li>
<li>Tools:
<ul>
<li>accessibility checkers
<ul>
<li><a href="https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=en">Accessibility Developer Tools</a> for Chrome</li>
<li><a href="http://www.deque.com/products/axe/">aXe: the Accessibility Engine</a> (<a href="https://chrome.google.com/webstore/detail/axe/lhdoppojpmngadmnindnejefpokejbdd?hl=en-US">chrome plugin</a> and <a href="https://github.com/dequelabs/axe-core">axe-core.js</a> - that can be used in your unit tests)</li>
</ul>
</li>
<li>Screen readers:
<ul>
<li><a href="http://www.nvaccess.org">NVDA</a> (it has text mode that prints output instead of converting it into speech: Tools -&gt; Speech viewer)</li>
<li><a href="http://www.freedomscientific.com/Products/Blindness/JAWS">JAWS</a></li>
<li><a href="http://windows.microsoft.com/en-us/windows/hear-text-read-aloud-narrator">Narrator</a></li>
</ul>
</li>
<li>Contrast:
<ul>
<li><a href="https://www.paciellogroup.com/resources/contrastanalyser/">Color contrast analyzer</a></li>
<li><a href="http://color.adobe.com">Color combinations matcher</a></li>
<li><a href="http://www.colourlovers.com/">Color pallets you can use for your website</a></li>
</ul>
</li>
</ul>
</li>
<li>W3C:
<ul>
<li><a href="https://www.w3.org/TR/wai-aria-practices/">Design patterns/best practices, WAI-ARIA</a> - when in doubt, check this succinct reference</li>
<li><a href="http://w3c.github.io/aria-in-html/">Using ARIA in HTML</a></li>
<li><a href="https://www.w3.org/TR/2014/REC-html5-20141028/dom.html#aria-usage-note">ARIA usage note</a> - When you should use aria-* and when you should NOT</li>
<li><a href="https://www.w3.org/TR/2011/CR-wai-aria-20110118/rdf_model.svg">[SVG] Role model diagram</a> - what aria properties/states apply to particular elements</li>
</ul>
</li>
</ul>
<h3>Summary</h3>
<p>If you are web developer you probably like when the tool you are using enables you to do everything without the mouse. This is thanks to keyboard accessibility, and smart focus management. If you play with color contrast analyzer you will notice that colors with good contrast are easier to read and simply just look better. Be aware that accessibility is about performance first. When your website is slow it can lead to unexpected focus behaviors, unwanted user actions, or moving content. How many times you tried to scroll to some part of website and it was moving because images were loading? I'm sure a lot.</p>
<p>What do you think? Is the website you are working on accessible? Have you ever even thought about it?</p>
<p><img class="aligncenter size-full wp-image-15131" src="{{ site.baseurl }}/assets/2016/08/accessibility_all_the_things.jpg" alt="Accessibility all the things" width="400" height="300" /></p>

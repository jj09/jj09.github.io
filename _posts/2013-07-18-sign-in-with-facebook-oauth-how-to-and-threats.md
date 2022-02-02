---
layout: post
title: 'Sign in with facebook (OAuth): how to and threats'
date: 2013-07-18 09:33:07.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- asp.net
- facebook
- oauth
- Open Source
- ruby
- Ruby on Rails
- security
- tutorial
meta:
  _yoast_wpseo_linkdex: '62'
  _edit_last: '1'
  _syntaxhighlighter_encoded: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _yoast_wpseo_focuskw: facebook oauth login
  _yoast_wpseo_metadesc: OAuth login with facebook tutorial for Rails and ASP.NET.
    Login with facebook threats.
  dsq_thread_id: '1509828134'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/sign-in-with-facebook-oauth-how-to-and-threats/"
---
<p>Many websites provide possibility to authorize with OAuth protocol (e.g. using facebook account). </p>
<h4>How to</h4>
<p>In ASP.NET application it is very easy to implement. Check <a href="http://www.asp.net/aspnet/overview/aspnet-45/oauth-in-the-default-aspnet-45-templates">this 3 minutes long screencast</a> by <a href="http://hanselman.com">Scott Hanselman</a>.</p>
<p>In Rails it is a little bit more complex, but also not big deal. There is nice <a href="http://railscasts.com/episodes/360-facebook-authentication?view=asciicast">Rails cast #360</a> about it (12 minutes).</p>
<h4>Threats</h4>
<p>However it is good to know what data we are providing when we click 'Login with facebook'. I implemented facebook auth with <a href="https://github.com/mkdynamic/omniauth-facebook">omniauth-facebook</a> library (according to above rails cast). I was surprised when I look at the source code.</p>
<p>This is auth data available for developer, when we sign in with facebook:</p>
<p>[ruby]{<br />
  :provider =&gt; 'facebook',<br />
  :uid =&gt; '1234567',<br />
  :info =&gt; {<br />
    :nickname =&gt; 'jbloggs',<br />
    :email =&gt; 'joe@bloggs.com',<br />
    :name =&gt; 'Joe Bloggs',<br />
    :first_name =&gt; 'Joe',<br />
    :last_name =&gt; 'Bloggs',<br />
    :image =&gt; 'http://graph.facebook.com/1234567/picture?type=square',<br />
    :urls =&gt; { :Facebook =&gt; 'http://www.facebook.com/jbloggs' },<br />
    :location =&gt; 'Palo Alto, California',<br />
    :verified =&gt; true<br />
  },<br />
  :credentials =&gt; {<br />
    :token =&gt; 'ABCDEF...', # OAuth 2.0 access_token, which you may wish to store<br />
    :expires_at =&gt; 1321747205, # when the access token expires (it always will)<br />
    :expires =&gt; true # this will always be true<br />
  },<br />
  :extra =&gt; {<br />
    :raw_info =&gt; {<br />
      :id =&gt; '1234567',<br />
      :name =&gt; 'Joe Bloggs',<br />
      :first_name =&gt; 'Joe',<br />
      :last_name =&gt; 'Bloggs',<br />
      :link =&gt; 'http://www.facebook.com/jbloggs',<br />
      :username =&gt; 'jbloggs',<br />
      :location =&gt; { :id =&gt; '123456789', :name =&gt; 'Palo Alto, California' },<br />
      :gender =&gt; 'male',<br />
      :email =&gt; 'joe@bloggs.com',<br />
      :timezone =&gt; -8,<br />
      :locale =&gt; 'en_US',<br />
      :verified =&gt; true,<br />
      :updated_time =&gt; '2011-11-11T06:21:03+0000'<br />
    }<br />
  }<br />
}[/ruby]</p>
<p>We provide our email(!), timezone and even location! Actually I was not aware of that. I thought facebook provides just basic info like name and photo. </p>
<p>We should think twice before we sign in to some website with OAuth. Especially due to providing our email address. Malicious websites can use it for sending spam.</p>

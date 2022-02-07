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

<h3>How to</h3>
<p>In ASP.NET application it is very easy to implement. Check <a href="http://www.asp.net/aspnet/overview/aspnet-45/oauth-in-the-default-aspnet-45-templates">this 3 minutes long screencast</a> by <a href="http://hanselman.com">Scott Hanselman</a>.</p>
<p>In Rails it is a little bit more complex, but also not big deal. There is nice <a href="http://railscasts.com/episodes/360-facebook-authentication?view=asciicast">Rails cast #360</a> about it (12 minutes).</p>

<h3>Threats</h3>
<p>However it is good to know what data we are providing when we click 'Login with facebook'. I implemented facebook auth with <a href="https://github.com/mkdynamic/omniauth-facebook">omniauth-facebook</a> library (according to above rails cast). I was surprised when I look at the source code.</p>
<p>This is auth data available for developer, when we sign in with facebook:</p>

{% highlight ruby %}
{
  :provider => 'facebook',
  :uid => '1234567',
  :info => {
    :nickname => 'jbloggs',
    :email => 'joe@bloggs.com',
    :name => 'Joe Bloggs',
    :first_name => 'Joe',
    :last_name => 'Bloggs',
    :image => 'http://graph.facebook.com/1234567/picture?type=square',
    :urls => { :Facebook => 'http://www.facebook.com/jbloggs' },
    :location => 'Palo Alto, California',
    :verified => true
  },
  :credentials => {
    :token => 'ABCDEF...', # OAuth 2.0 access_token, which you may wish to store
    :expires_at => 1321747205, # when the access token expires (it always will)
    :expires => true # this will always be true
  },
  :extra => {
    :raw_info => {
      :id => '1234567',
      :name => 'Joe Bloggs',
      :first_name => 'Joe',
      :last_name => 'Bloggs',
      :link => 'http://www.facebook.com/jbloggs',
      :username => 'jbloggs',
      :location => { :id => '123456789', :name => 'Palo Alto, California' },
      :gender => 'male',
      :email => 'joe@bloggs.com',
      :timezone => -8,
      :locale => 'en_US',
      :verified => true,
      :updated_time => '2011-11-11T06:21:03+0000'
    }
  }
}
{% endhighlight %}

<p>We provide our email(!), timezone and even location! Actually I was not aware of that. I thought facebook provides just basic info like name and photo. </p>

<p>We should think twice before we sign in to some website with OAuth. Especially due to providing our email address. Malicious websites can use it for sending spam.</p>

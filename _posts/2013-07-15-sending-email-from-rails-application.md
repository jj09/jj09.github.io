---
layout: post
title: Sending email from Rails application
date: 2013-07-15 09:22:21.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- ruby
- Ruby on Rails
meta:
  _edit_last: '1'
  _syntaxhighlighter_encoded: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _yoast_wpseo_linkdex: '63'
  _yoast_wpseo_focuskw: ActionMaier, send, email, Ruby, Rails
  _yoast_wpseo_metadesc: Send email in Ruby on Rails application - tutorial / example.
  dsq_thread_id: '1502071511'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/sending-email-from-rails-application/"
---
<p>It took me a while to configure sending email from Rails application. I went through many different tutorials, blogs, StackOverflow posts etc. Step, by step I found working configuration.</p>
<p>To send emails I use <em>ActionMailer</em>. First you need to generate mailer:</p>
<p><code>rails generate mailer UserMailer</code></p>
<p>It will create <em>UserMailer</em> class in <em>app/mailers</em> directory. In this class we need to define our method for sending emails:</p>
<p>[ruby]class UserMailer &lt; ActionMailer::Base<br />
  default from: &quot;from@example.com&quot;</p>
<p>  def send_email(user_email, content)<br />
  	@user_email = user_email<br />
  	@content = content<br />
  	mail(to: &quot;your@mail.com&quot;, subject: &quot;Email from mysite.com&quot;)<br />
  end<br />
end[/ruby]</p>
<p>Then in the directory <em>app/views/user_mailer</em> we need to create template for our email: <em>send_email.html.erb</em> (this name must match the name of action created in <em>UserMailer</em> class):</p>
<p>[html]&lt;!DOCTYPE html&gt;<br />
&lt;html&gt;<br />
  &lt;head&gt;<br />
    &lt;meta content='text/html; charset=UTF-8' http-equiv='Content-Type' /&gt;<br />
  &lt;/head&gt;<br />
  &lt;body&gt;<br />
    &lt;p&gt;<br />
      From: &lt;%= @user_email %&gt;<br />
    &lt;/p&gt;<br />
    &lt;p&gt;<br />
      &lt;%= @content %&gt;<br />
    &lt;/p&gt;<br />
  &lt;/body&gt;<br />
&lt;/html&gt;[/html]</p>
<p>(*) If you do not want to send html you can create plain text and name file <em>send_email.text.erb</em>.</p>
<p>Now, the hardest part. Configuration of smtp. You need to add it to <em>config/environments/development.rb</em> (or <em>test.rb</em> or <em>production.rb</em>). I found this configuration working for gmail:</p>
<p>[ruby]# set delivery method to :smtp, :sendmail or :test<br />
  config.action_mailer.delivery_method = :smtp<br />
  config.action_mailer.perform_deliveries = true</p>
<p>  # these options are only needed if you choose smtp delivery<br />
  config.action_mailer.smtp_settings = {<br />
    :address        =&gt; 'smtp.gmail.com',<br />
    :port           =&gt; 587,<br />
    :domain         =&gt; 'gmail.com',<br />
    :authentication =&gt; :login,<br />
    :user_name      =&gt; 'your_gmail@gmail.com',<br />
    :password       =&gt; 'your_password',<br />
    :enable_starttls_auto =&gt; true<br />
  }[/ruby]</p>
<p>The last thing is call <em>ActionMailer</em> from our app:</p>
<p>[ruby]UserMailer.send_email(params[:from], params[:content]).deliver[/ruby]</p>
<p>Form for sending email can looks like that:<br />
[html]&lt;%= form_tag '/send_email', method: 'post' do %&gt;<br />
	&lt;div class=&quot;field&quot;&gt;<br />
		Email&lt;br /&gt;<br />
    &lt;%= email_field_tag :from %&gt;<br />
  &lt;/div&gt;</p>
<p>	&lt;div class=&quot;field&quot;&gt;<br />
		Content&lt;br /&gt;<br />
    &lt;%= text_area_tag :content, nil, rows: 10, cols: 25 %&gt;<br />
  &lt;/div&gt;</p>
<p>  &lt;div class=&quot;actions&quot;&gt;<br />
    &lt;%= submit_tag &quot;Send&quot;, class: &quot;btn btn-large btn-primary&quot; %&gt;<br />
  &lt;/div&gt;<br />
&lt;% end %&gt;[/html]</p>
<p>For that you need to configure action in controller and match route e.g.:</p>
<p>[ruby]match '/send_email', to: 'your_controller#your_action'[/ruby]</p>
<p>Method <em>send_mail</em> (from <em>UserMailer</em> class) can have as much parameters as you need. It can be also 0. In above example, the params are just rendered in the email template (send_email.html.erb file).</p>
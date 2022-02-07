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

{% highlight ruby %}
class UserMailer < ActionMailer::Base
  default from: "from@example.com"
  def send_email(user_email, content)
  	@user_email = user_email
  	@content = content
  	mail(to: "your@mail.com", subject: "Email from mysite.com")
  end
end
{% endhighlight %}

<p>Then in the directory <em>app/views/user_mailer</em> we need to create template for our email: <em>send_email.html.erb</em> (this name must match the name of action created in <em>UserMailer</em> class):</p>
{% highlight html %}
<!DOCTYPE html>
<html>
  <head>
    <meta content='text/html; charset=UTF-8' http-equiv='Content-Type' />
  </head>
  <body>
    <p>
      From: <%= @user_email %>
    </p>
    <p>
      <%= @content %>
    </p>
  </body>
</html>
{% endhighlight %}
<p>(*) If you do not want to send html you can create plain text and name file <em>send_email.text.erb</em>.</p>
<p>Now, the hardest part. Configuration of smtp. You need to add it to <em>config/environments/development.rb</em> (or <em>test.rb</em> or <em>production.rb</em>). I found this configuration working for gmail:</p>


{% highlight ruby %}
# set delivery method to :smtp, :sendmail or :test
  config.action_mailer.delivery_method = :smtp
  config.action_mailer.perform_deliveries = true
  # these options are only needed if you choose smtp delivery
  config.action_mailer.smtp_settings = {
    :address        => 'smtp.gmail.com',
    :port           => 587,
    :domain         => 'gmail.com',
    :authentication => :login,
    :user_name      => 'your_gmail@gmail.com',
    :password       => 'your_password',
    :enable_starttls_auto => true
  }
{% endhighlight %}

<p>The last thing is call <em>ActionMailer</em> from our app:</p>


{% highlight ruby %}
UserMailer.send_email(params[:from], params[:content]).deliver
{% endhighlight %}

<p>Form for sending email can looks like that:

{% highlight html %}
<%= form_tag '/send_email', method: 'post' do %>
	<div class="field">
		Email
    <%= email_field_tag :from %>
  </div></p>
<p>	<div class="field">
		Content
    <%= text_area_tag :content, nil, rows: 10, cols: 25 %>
  </div></p>
<p>  <div class="actions">
    <%= submit_tag "Send", class: "btn btn-large btn-primary" %>
  </div>
<% end %>
{% endhighlight %}

<p>For that you need to configure action in controller and match route e.g.:</p>

{% highlight ruby %}
match '/send_email', to: 'your_controller#your_action'
{% endhighlight %}

<p>Method <em>send_mail</em> (from <em>UserMailer</em> class) can have as much parameters as you need. It can be also 0. In above example, the params are just rendered in the email template (send_email.html.erb file).</p>

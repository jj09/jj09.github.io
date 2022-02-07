---
layout: post
title: Ninja Rails Developer
date: 2013-07-23 11:06:51.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
- tools
tags:
- developer
- ruby
- Ruby on Rails
- SublimeText
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _yoast_wpseo_linkdex: '68'
  _yoast_wpseo_focuskw: rails developer environment
  _yoast_wpseo_metadesc: Rails Developer Environment Configuration
  dsq_thread_id: '1523932354'
  _syntaxhighlighter_encoded: '1'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/ninja-rails-developer/"
---
<p><i>Warning: this configuration was tested only on MacOS X.</i></p>
<p>To create default project in Rails we just need to run command:</p>
<p><code>rails new my_app</code> </p>
<p>However it creates project without many useful gems. I found nice Gem-set and some configuration hacks in <a href="http://ruby.railstutorial.org/">Michael Hartl's tutorial</a>.</p>
<p>Instead of standard test framework (TestUnit) he use <a href="http://rspec.info/">RSpec</a> (which is more popular among Rails developers). To generate project without standard test, run command:</p>
<p><code>rails new my_app --skip-test-unit</code> </p>
<p>Then use his <a href="https://raw.github.com/railstutorial/sample_app_2nd_ed/master/Gemfile">Gemfile</a> (this link is kept up to date). Copy it a paste into <em>my_app/Gemfile</em>. I recommend to uncomment everything (to use all Gems from the file).</p>
<p>Once <em>Gemfile</em> is modified, you need to install gems:</p>
<p><code>bundle install</code></p>
<p>Then you can run RSpec test:</p>
<p><code>bundle exec rspec</code> </p>
<p>You may need to point the tests' directory:</p>
<p><code>bundle exec rspec rspec/</code> </p>
<p>It would be nice to run them with just 'rspec' command. To do that we need to run following commands (if we used RVM to install Rails):</p>
<p><code>rvm get head && rvm reload</code> </p>
<p><code>cd ~/projects/my_app</code> </p>
<p><code>bundle install --without production --binstubs=./bundler_stubs</code> </p>
<p>After those steps you should be able to run RSpec with:</p>
<p><code>rspec</code> </p>
<p>You should get a warning, that to maintain this possibility you need to add following line to <em>~/.bash_profile</em> if it exists, otherwise add it to <em>~/.bash_login</em>:</p>
<p><code>source ~/.profile</code> </p>
<p>Michael Hartl's Gem file contains 'guard'. It allows us to run RSpec test each time, when we change some file (after save). </p>
<p>To initialize guard (if all above steps are performed, otherwise you need to add 'bundle exec ' at the beginning):</p>
<p><code>guard init</code> </p>
<p>It creates <em>Guardfile</em> in main project directory, which specify when tests should be run (which files should be monitored). To run guard:</p>
<p><code>guard</code> </p>
<p>The last improvement is use the test server <a href="https://github.com/sporkrb/spork">Spork</a>. It allows to run tests faster. Without Spork, RSpec needs to reload entire Rails environment before run the tests (in each run). Spork loads the environment once, and then maintains a pool of processes for running future tests. Unfortunately it works only on POSIX systems (which means: doesn't work on Windows).</p>
<p>To setup spork run:</p>
<p><code>spork --bootstrap</code></p>

<p>Then change <em>spec/spec_helper.rb</em> file to something like that:</p>
{%highlight ruby %}
require 'rubygems'
require 'spork'
Spork.prefork do
  ENV["RAILS_ENV"] ||= 'test'
  require File.expand_path("../../config/environment", __FILE__)
  require 'rspec/rails'
  require 'rspec/autorun'
  Dir[Rails.root.join("spec/support/**/*.rb")].each {|f| require f}
  RSpec.configure do |config|
    config.mock_with :rspec
    config.fixture_path = "#{::Rails.root}/spec/fixtures"
    config.use_transactional_fixtures = true
    config.infer_base_class_for_anonymous_controllers = false
  end
end
Spork.each_run do
  # This code will be run each time you run your specs.
end
{% endhighlight %}

<p>You also need to configure RSpec to automatically use Spork. To do that, modify .rspec file:</p>
{% highlight txt %}
--color
--drb
{% endhighlight %}
<p>To run Spork:</p>
<p><code>spork</code></p>
<p>You can test difference between running tests with and without spork.</p>
<p><code>time rspec</code></p>
<p>In my case it was 4.821s without Spork, and 0.784 with Spork.</p>
<p>The disadvantage of Spork is that after e.g. changes in database we need to restart it. </p>
<p>The screencast showing advanced setup by Michael Hartl is available for free <a href="http://youtu.be/FZ-b9oZpCZY">here</a>. If you use SublimeText (as I do), you can follow <a href="http://youtu.be/05x1Jk4rT1A">this screencast</a> to adjust it for Rails development. After that you will be able even to run tests from SublimeText!</p>

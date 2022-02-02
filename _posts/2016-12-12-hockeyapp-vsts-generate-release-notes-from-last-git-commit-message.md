---
layout: post
title: "[HockeyApp + VSTS] Generate release notes from last git commit message"
date: 2016-12-12 15:17:10.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- HockeyApp
- VSTS
- Xamarin
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
  dsq_thread_id: '5375714585'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/hockeyapp-vsts-generate-release-notes-from-last-git-commit-message/"
---
<p>Continuous Integration and Continuous delivery for Xamarin apps with VSTS and HockeyApp is awesome!</p>
<p>I blogged about <a href="http://jj09.net/continuous-integration-and-continuous-delivery-for-xamarin-ios-with-vsts/">setting up CI/CD pipeline with VSTS+HockeyApp</a> a few weeks ago.</p>
<p>If you want to add release notes to HockeyApp release you have two options:</p>
<ol>
<li>Add release notes manually, by setting 'Release Notes' property, and update them before every build (AKA - option that sucks)</li>
<li>Add path to release notes file, by setting 'Release Notes (file)' property, and update it before every git push (AKA - option that sucks less)</li>
<li>Add path to release notes file, by setting 'Release Notes (file)' property, and generate release notes from last git commit message on every build (AKA - option that rocks)</li>
</ol>
<p>Applying options 1 and 2 is easy.</p>
<p>To make option 3 happen you need to add script that will get last git commit message, and output it to the file that you specified in 'Release Notes (file)' property. This script should be executed before 'Deploy to HockeyApp' step (of course).</p>
<p>For Xamarin.iOS you need to add 'Shell Script' task that can look like this:</p>
{% highlight shell %}
echo "last commit: $BUILD_SOURCEVERSIONMESSAGE" > commit.txt
{% endhighlight %}
<p>*it will output file to the same directory where shell script is located</p>
<p>For Xamarin.Droid and Windows builds, you can create <a href="http://stackoverflow.com/questions/38199473/how-to-retrieve-git-commit-id-and-message-in-vsts-tfs-build/38200972">PowerShell script</a>.</p>

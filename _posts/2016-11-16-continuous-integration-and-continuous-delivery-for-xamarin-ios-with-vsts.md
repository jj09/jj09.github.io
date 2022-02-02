---
layout: post
title: Continuous Integration and Continuous Delivery for Xamarin.iOS with VSTS (Vistul
  Studio Team Services)
date: 2016-11-16 15:26:16.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
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
  dsq_thread_id: '5309948747'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/continuous-integration-and-continuous-delivery-for-xamarin-ios-with-vsts/"
---
<p>Visual Studio Team Services has great Continuous Integration and Continues Delivery support for Xamarin.</p>
<p>Recently I was configuring pipeline that would build the project, run unit tests (with xUnit), run UI tests (with Xamarin Test Cloud), and, if all tests pass, deploy new version of the app to Hockey App. During the process of creating VSTS build definition I encountered a few problems that I think are worth to share with you.</p>
<p>To make a basic build definition with building Xamarin.iOS project and deploying to Hockey App with VSTS+Xamarin check James Montemagno's <a href="https://blog.xamarin.com/continuous-integration-for-ios-apps-with-visual-studio-team-services/">Continuous Integration for iOS Apps with Visual Studio Team Services</a> first.</p>
<p>The issues I had, that were not described anywhere online:</p>
<ul>
<li>I couldn't use "Visual Studio Test" task for running xUnit tests, because every build definition on VSTS can be executed by only one build agent, and to build Xamarin project I needed Mac build agent.</li>
<li>How to run UI tests (with Xamarin Test Cloud) using the same build that would be later on deployed to Hockey App? Test Cloud requires init code that later on shouldn't be present in deployed app.</li>
</ul>
<h3>Running xUnit tests with Mac build agent</h3>
<p>This requires adding 2 tasks to build definition:</p>
<ol>
<li>Command Line task - to run tests with mono and xUnit console runner.</li>
<li>Publish Test Results task - to display results in build summary</li>
</ol>
<p>First, install xUnit console runner NuGet package.</p>
<p>To run tests, add command line task with following settings:</p>
<ul>
<li>Tool: <em>mono</em></li>
<li>Arguments: <em>packages/xunit.runner.console.<strong>2.1.0</strong>/tools/xunit.console.exe <strong>YourApp</strong>.UnitTests/bin/Debug/<strong>YourApp</strong>.UnitTests.dll -xml UnitTestsResults.xml</em></li>
</ul>
<p>Remember to replace <em>YourApp</em> with your app name, and set the same xUnit runner version that you have installed.</p>
<p>To publish test results, add "Publish Test Results" task with the following settings:</p>
<ul>
<li>Test Result Format: <em>XUnit</em></li>
<li>Test Result Files: <em>**/UnitTestsResults.xml</em></li>
<li>Always run: <em>true</em></li>
</ul>
<h3>Running Xamarin UI tests with Test Cloud before deploying to HockeyApp</h3>
<p>The solution there is rather simple: build in Debug mode that has <em>TEST_CLOUD</em> preprocessor directive defined, run tests, and then build again in Release mode before deploying to Hockey App.</p>
<h3>Delete files before build</h3>
<p>For a while I couldn't figure out why my tests are not passing when run from VSTS while they pass on my machine. It turned out, VSTS was using old builds for tests. I am not sure about <a href="https://www.macincloud.com/">MacInCloud</a>, but if you are using your own Build Agent running on your Mac the directories that contains binary files are not being cleaned up before next build automatically. To avoid using old builds, you can add, at the beginning of your pipeline, "Delete Files" task and delete everything from bin/* and obj/*.</p>
<h3>Summary</h3>
<p>The final build definition looks like that:</p>
<p><img class="aligncenter size-full wp-image-16291" src="{{ site.baseurl }}/assets/2016/11/AzureStatusBuildDefinition.png" alt="Azure Status VSTS build definition" width="687" height="657" /></p>
<p>Let me know if I missed some details! I would be happy to add them! Also - if you know better way of doing that - let me know as well!</p>

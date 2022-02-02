---
layout: post
title: Compiling TypeScript files on Azure Web Apps
date: 2016-08-31 11:43:15.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- Azure
- TypeScript
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
  dsq_thread_id: '5109532141'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/compiling-typescript-files-on-azure-web-apps/"
---
<p>Your TypeScript project shouldn't have JavaScript files in the repository. It may be problematic when you want to deploy your site from <a href="http://jj09.net/azure-portal-tips-tricks-15-deploying-website-with-git/">git repo on Azure Web Apps</a>. You may consider adding some custom scripts, but there is a better way: use <code>npm postinstall</code>.</p>
<p>I have created a simple TypeScript project, put it on <a href="https://github.com/jj09/tsc-postinstall">github</a>, and deployed to <a href="http://tscpostinstall.azurewebsites.net/">tscpostinstall.azurewebsites.net</a></p>
<p>You can check out how to deploy Azure Web App from github in one of my <a href="http://aka.ms/azuretipsandtricks">Azure Tips &amp; Tricks</a> videos:</p>
<p><iframe src="https://www.youtube.com/embed/dWvZz9zB7ck" width="640" height="360" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>

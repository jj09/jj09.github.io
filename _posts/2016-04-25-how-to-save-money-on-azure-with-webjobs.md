---
layout: post
title: How to save money on Azure with WebJobs
date: 2016-04-25 21:33:35.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- blog
- programming
tags:
- Azure
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
  _oembed_bc5873f0aab3843b5891405b9ea29b9e: "{{unknown}}"
  builder_switch_frontend: '0'
  dsq_thread_id: '4777162708'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/how-to-save-money-on-azure-with-webjobs/"
---
<p>This blog is hosted on Azure. It is using WordPress, which stores its data in MySQL database hosted by ClearDb. I <a title="WordPress on Azure: Exceeded ClearDB size = lock on INSERT/UPDATE (not able to log in to the admin panel)" href="http://jj09.net/wordpress-on-azure-exceeded-cleardb-size-lock-on-insert-update/">blogged about the issues with WordPress database size</a> over a year ago. The issue is inserting transient entries into database that are growing its size and exceeding free 20MB ClearDB limit. As I mentioned in <a href="http://jj09.net/wordpress-on-azure-exceeded-cleardb-size-lock-on-insert-update/">this</a> blog post - you can use plugins that clear database for you, or...you can use web jobs. <a href="http://azure.microsoft.com/en-us/documentation/articles/websites-webjobs-resources/">Azure WebJobs</a> is very neat way to perform custom tasks, such as database maintenance, periodically.</p>
<p>I created a web job that is performing database maintenance for me. Everyday it <a href="http://stackoverflow.com/questions/10422574/can-i-remove-transients-in-the-wp-options-table-of-my-wordpress-install">removes 'transient' entries from wp_options table</a> to keep my MySQL database under 20MB ClearDB limit.</p>
<p>One problem was: how to do MySQL backup without <a href="http://dev.mysql.com/doc/refman/5.1/en/mysqldump.html">mysqldump</a>? As you know, there is a Virtual Machine underneath every Azure website. And this VM has MySQL, along with mysqldump installed:</p>
<p><img class="aligncenter size-full wp-image-8541" src="{{ site.baseurl }}/assets/2016/04/azure-console-mysqldump.jpg" alt="Azure Console: mysqldump" width="399" height="1031" /></p>
<p>Based on <a href="http://www.codeproject.com/Articles/43438/Connect-C-to-MySQL">this article</a> I created a small Console App called <a href="https://github.com/jj09/DbMaintenance">DbMaintenance</a> that performs 3 mentioned tasks:</p>
<ol>
<li>Backup database</li>
<li>Remove transient entries from <code>wp_options</code> table.</li>
<li>Backup database</li>
</ol>
<p>Two backups gives me more confidence that I have my database backed up correctly. Especially because I am performing them before and after the operation that potentially can broke things.</p>
<p>You can customize <a href="https://github.com/jj09/DbMaintenance">my app</a> by editing <code>Initialize</code> method. Current paths (for mysqldump and database backup directory) are set for Azure Website. Additionally you have to create directory for backups (<code>D:\home\db-backups</code>). You can do it from the web app console available on the <a href="http://portal.azure.com">Azure Portal</a>:</p>
<p><code>mkdir D:\home\db-backup</code></p>
<p>Once this is done, you need to zip DbMaintenance.exe and MySql.Data.dll file, and create a WebJob. On the Azure Portal go to your web app -&gt; Settings -&gt; WebJobs, and add a new WebJob:</p>
<p><img class="aligncenter size-full wp-image-8561" src="{{ site.baseurl }}/assets/2016/04/azure_portal-add-WebJob.jpg" alt="Azure Portal: add WebJob" width="301" height="427" /></p>
<p>You can see the status in Settings -&gt; WebJobs -&gt; YOUR_JOB_NAME:</p>
<p><img class="aligncenter size-full wp-image-8601" src="{{ site.baseurl }}/assets/2016/04/azure-webjobs.jpg" alt="azure webjobs" width="566" height="290" /></p>
<p>By clicking on logs column, you can get details about web job:</p>
<p><img class="aligncenter size-full wp-image-8611" src="{{ site.baseurl }}/assets/2016/04/azure-webjob-details.jpg" alt="Azure WebJob: details" width="726" height="454" /></p>
<p>And console output from each execution:</p>
<p><img class="aligncenter size-full wp-image-8621" src="{{ site.baseurl }}/assets/2016/04/azure-webjob-details-console_output.jpg" alt="Azure WebJob: console output" width="722" height="590" /></p>
<p>I configured my WebJob to run everyday. You can also run it on demand, or continuously.</p>
<p>You can find more about Azure WebJobs <a href="http://azure.microsoft.com/en-us/documentation/articles/web-sites-create-web-jobs/">in this article</a>.</p>

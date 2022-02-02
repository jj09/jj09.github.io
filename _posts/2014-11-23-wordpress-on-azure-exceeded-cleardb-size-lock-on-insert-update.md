---
layout: post
title: 'Wordpress on Azure: Exceeded ClearDB size = lock on INSERT/UPDATE (not able
  to log in to the admin panel)'
date: 2014-11-23 19:42:32.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- Azure
- ClearDB
- cloud
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
  _syntaxhighlighter_encoded: '1'
  builder_switch_frontend: '0'
  dsq_thread_id: '3256752684'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/wordpress-on-azure-exceeded-cleardb-size-lock-on-insert-update/"
---
<p>My Wordpress blog is hosted on Windows Azure, and I am using the only MySQL provider that is available on Azure: ClearDB.</p>
<p>Yesterday I couldn't log in to the admin panel. I had no idea what was going on, because blog was working. I was googling for cause/solution, checking Azure logs, monitoring on Azure Portal, and accidentally I noticed that I exceeded ClearDB quota (20 MB). I did not receive any notifications from ClearDB though. What is important: if you exceed this limit, they block INSERT and UPDATE operations. My guess is that Wordpress is probably trying to INSERT/UPDATE something in database when you log in. That's why I couldn't log in.</p>
<p>I did not want to upgrade from free instance to $9.99/month (the cheapest upgrade option). Fortunately I was able to connect with database using MySQL Workbench, and optimize my database.</p>
<p>I removed post revisions:</p>
<p>[sql]DELETE FROM wp_posts WHERE post_type = &quot;revision&quot;;[/sql]</p>
<p>And <a href="http://codex.wordpress.org/Transients_API">transients</a>:</p>
<p>[sql]DELETE FROM wp_options WHERE option_name LIKE ('%\_transient\_%')[/sql]</p>
<p>This allowed me to save a lot of space. From 20.28 MB, the database size went to 10.42 MB (transients occupied almost 8MB!):</p>
<p>&nbsp;</p>
<p><img class="aligncenter size-full wp-image-7171" src="{{ site.baseurl }}/assets/2014/11/cleardb-quota.png" alt="ClearDB quota" width="261" height="172" /></p>
<p>After I did that, I was able to log in. However, INSERT/UPDATE lock is not revoked immediately. I had to wait something between 10 minutes and 2 hours. I went to the swimming pool in meantime, thus I am not sure how much exactly it take.</p>
<p>Useful SQL command to check you database size:</p>
<p>[sql]SELECT SUM(round(((data_length + index_length) / 1024 / 1024), 2)) &quot;Size in MB&quot;<br />
FROM information_schema.TABLES<br />
WHERE table_schema = '$DB_NAME'<br />
ORDER BY (data_length + index_length) DESC;[/sql]</p>
<p>You can also check each table size:</p>
<p>[sql]SELECT table_name AS &quot;Tables&quot;,<br />
round(((data_length + index_length) / 1024 / 1024), 2) &quot;Size in MB&quot;<br />
FROM information_schema.TABLES<br />
WHERE table_schema = '$DB_NAME'<br />
ORDER BY (data_length + index_length) DESC;[/sql]</p>
<p>For the future, I pinned the database size tile to my Azure Portal dashboard. Now, I will be able to see it every time I am visiting the portal. I also limited the number of post/pages revisions to 2, by editing <em>wp-config.php</em> file, and inserting this line:</p>
<p>[php]define('WP_POST_REVISIONS', 2);[/php]</p>
<p>This should be enough to not exceed the quota for some time, but I will need some permanent solution. I am thinking about <a href="http://www.stefangordon.com/migrate-azure-wordpress-mysql-database-to-azure-vm/">hosting my own MySQL database on LinuxVM, on Azure</a> (cost: $13+).</p>
<p>During the troubleshooting I found very good blog post by John Papa: <a href="http://www.johnpapa.net/azurecleardbmysql/">Tips for WordPress on Azure</a>. I recommend you to check this out if you have a Wordpress blog on Azure. <a href="http://premium.wpmudev.org/blog/optimizing-your-wordpress-database-a-complete-guide/">This article</a> will help you to optimize your Wordpress database as well.</p>
<p><strong>EDIT</strong>: The plugin <a href="https://wordpress.org/plugins/rvg-optimize-database/">Optimize Database after Deleting Revisions</a> allow to clean up database even more efficient. I managed to slim my DB down by another 50%, to 4.11., which gives almost 80% size decrease from the original 20+ MB.</p>
<p><img class="aligncenter size-full wp-image-7341" src="{{ site.baseurl }}/assets/2014/11/cleardb-quota-with-plugin.png" alt="ClearDB quota with plugin" width="244" height="161" /></p>
<p>What is even more cool about this plugin, you can create a schedule to run it automatically (Settings -&gt; Optimize DB options):</p>
<p><img class="aligncenter size-full wp-image-7361" src="{{ site.baseurl }}/assets/2014/11/optimize-db-plugin.png" alt="Optimize Database after Deleting Revisions - Options" width="800" height="341" /></p>

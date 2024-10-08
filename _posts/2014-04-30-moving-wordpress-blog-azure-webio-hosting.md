---
layout: post
title: Moving WordPress blog to Azure from Webio hosting
date: 2014-04-30 23:19:19.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- blog
tags:
- Azure
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
  dsq_thread_id: '2651855690'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/moving-wordpress-blog-azure-webio-hosting/"
---
<p><img class="aligncenter size-full wp-image-1441" src="{{ site.baseurl }}/assets/2014/04/azure_logo.jpg" alt="Microsoft Azure" width="400" height="200" /></p>
<p>I decided to move my blog from hosting on <a href="http://webio.pl">Webio.pl</a> to Microsoft Azure (<a href="http://blogs.msdn.com/b/windowsazure/archive/2014/03/25/upcoming-name-change-for-windows-azure.aspx">formerly Windows Azure before March, 25th 2014</a>). Why? To get more familiar with the Cloud and especially Azure.</p>
<p>I did my migration following <a href="http://www.davebost.com/">Dave Bost's</a> series <a href="http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1">Moving a WordPress Blog to Windows Azure</a>:</p>
<ul>
<li><a href="http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1">Part 1: Creating a WordPress Blog on Windows Azure</a></li>
<li><a href="http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content">Part 2: Transferring Your Content</a></li>
<li><a href="http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain">Part 3: Setting Up Your Custom Domain</a></li>
<li><a href="http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules">Part 4: Pretty Permalinks and URL Rewrite rules</a></li>
<li><a href="http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root">Part 5: Moving From a Subfolder to the Root</a></li>
</ul>
<p>However, not everything went smoothly and easy. Additionally, I adjusted some steps to my needs/settings/plugins/hosting(Webio).</p>
<h3>Small adjustments</h3>
<p>Instead of <a href="http://blogs.msdn.com/b/avkashchauhan/archive/2012/06/19/windows-azure-website-uploading-downloading-files-over-ftp-and-collecting-diagnostics-logs.aspx">connecting through FTP to copy content (uploads/themes/plugins)</a>, I used <a href="https://wordpress.org/plugins/updraftplus/">UpdraftPlus</a> plugin. Moreover, I am using it for weekly backups all the time. It is really nice, especially the cloud backup option, which allows me to put backup files into my Dropbox automatically.</p>
<p>To <a href="http://codex.wordpress.org/Backing_Up_Your_Database">export my database</a> I used phpMyAdmin provided by Webio. As <a href="http://wordpress.org/plugins/portable-phpmyadmin/description/">Portable phpMyAdmin</a> plugin is no longer available, I took advantage of <a href="https://wordpress.org/plugins/adminer/">Adminer</a> plugin to import database on Azure. Another option is to <a href="http://ruslany.net/2012/12/phpmyadmin-on-windows-azure-web-sites/">install phpMyAdmin on Azure</a>.</p>
<p>I am using <a href="http://themify.me/themes/itheme2">iTheme2</a> template, which allows to export customized settings (iTheme2/import tab). After migration, you can easily import it going to the same place.</p>
<p>I had bunch of themes installed. I was testing/experimenting with them <a href="http://jj09.net/hello-world/">when I started my blog</a>. It took me a while to find a way to remove installed theme. You need to go to Appearance/Themes, click on theme you want to remove and then click delete button in right, bottom corner. I deleted all themes, but my current one (iTheme2) and Twenty-* themes.</p>
<p><img class="aligncenter size-full wp-image-1501" src="{{ site.baseurl }}/assets/2014/04/wordpress_delete_theme.png" alt="WordPress - Delete theme" width="600" height="422" /></p>
<h3>Webio specific</h3>
<p>Specific for any hosting provider is setting the custom domain. In order to do that on Webio, you need to go to Domains/Edit DNS entries (in polish: Domeny/Edytuj wpisy w strefie DNS tej domeny). In the image below, there are DNS entries for my domain. Only highlighted entries matters for redirecting domain to Azure:</p>
<p><a href="http://jj09.net/wp-content/uploads/2014/04/webio_dns_settings.png"><img class="aligncenter size-large wp-image-1491" src="{{ site.baseurl }}/assets/2014/04/webio_dns_settings-785x451.png" alt="Webio DNS settings" width="785" height="451" /></a></p>
<p>When you add domain entries in Azure you need to add www.* entry separately (in my case: jj09.net and www.jj09.net). More details can be found <a href="http://azure.microsoft.com/en-us/documentation/articles/web-sites-custom-domain-name/">here</a>.</p>
<p><img class="aligncenter size-full wp-image-1481" src="{{ site.baseurl }}/assets/2014/04/azure_manage_custom_domains.jpg" alt="Azure - manage custom domains" width="644" height="396" /></p>
<p>Remember to create/update web.config file, in order to make your custom domain and permalinks (if you use them) working correctly (as mentioned in <a href="http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root">part 5</a> of <a href="http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1">Dave Bost's tutorial</a>):</p>
{% highlight xml %}
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
	<system.webServer>
		<rewrite>
			<rules>
				<rule name="Main Rule" stopProcessing="true">
					<match url=".*"/>
					<conditions logicalGrouping="MatchAll">
						<add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true"/>
						<add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true"/>
					</conditions>
					<action type="Rewrite" url="index.php"/>
				</rule>
			</rules>
		</rewrite>
	</system.webServer>
</configuration>
{% endhighlight %}
<h3>Issues</h3>
<p>When I was trying to set <a href="http://www.wpbeginner.com/plugins/how-to-send-email-in-wordpress-using-the-gmail-smtp-server/">SMTP server to my gmail</a> I received following email from Google, after try to send test email:</p>
<p><img class="aligncenter size-full wp-image-1511" src="{{ site.baseurl }}/assets/2014/04/GoogleHijackWarning.png" alt="Google hijack warning" width="576" height="463" /></p>
<p>After following steps in provided link, the issue was fixed. There is one interesting thing: I set region for my website to WestUS. However, Google says: "Location: Spain". Hmm...</p>
<p>Another issue I had was getting 404 error on .woff file (<a href="https://wordpress.org/plugins/crayon-syntax-highlighter/">Crayon Syntax Highlighter</a> plugin font file). I solved it, by modifying web.config file as described <a href="http://stackoverflow.com/questions/4015816/why-is-font-face-throwing-a-404-error-on-woff-files">here</a>.</p>
<p>I had also problem with <a href="https://wordpress.org/plugins/only-tweet-like-share-and-google-1/">Tweet, Like, Google +1 and Share</a> plugin. It dosn't display buttons on home page. I tried some tricks (deactivate, re-install) to solve it, but I didn't succeed.</p>
<h3>Pricing</h3>
<p>For hosting on <a href="http://webio.pl">Webio.pl</a> I was paying around $20/year (<a href="https://www.webio.pl/hosting-asp-net/plan-startowy.html">start plan</a>). On Azure, I will need to pay at least $10/month for shared instance (required to have domain <a href="http://jj09.net">jj09.net</a>), which is $120/year. 6x more expensive! Am I crazy? No. As I stated at the beginning, I want to play with Azure. When I decide I am done with that, I can always go back to <a href="http://webio.pl">Webio.pl</a> or some other hosting.</p>
<p>After one week, my estimated bill is  2,07 €.</p>

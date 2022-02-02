---
layout: post
title: Brute Force Attack on my blog
date: 2014-09-02 19:31:52.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- blog
- security
tags:
- brute force
- hacking
- WordPress
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
  dsq_thread_id: '2982837724'
  _wp_old_slug: brute-force-attack-blog
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/brute-force-attack-on-my-blog/"
---
<p>Some time ago I created an Azure alert (thanks to <a href="http://irisclasson.com/2014/07/14/setting-up-azure-alert-rules/">Iris Classon</a>). I did it as a part of my Azure exploration. The rule I created, send me email every time I have more than 1000 requests per hour:</p>
<p><img class="aligncenter size-full wp-image-4631" src="{{ site.baseurl }}/assets/2014/09/azure-alert.jpg" alt="azure alert" width="600" height="472" /></p>
<p>I received one or two e-mails in last two weeks and that was fine. High traffic can happen occasionally. Of course I created this rule based on history of the number of requests from the past. However, last night I received 3 e-mails. I checked with Azure Management Portal and number of requests suddenly exploded:</p>
<p><img class="aligncenter size-full wp-image-4701" src="{{ site.baseurl }}/assets/2014/09/azure-alert-requests.jpg" alt="azure alert requests" width="931" height="267" /></p>
<p>That was suspicious. To make an investigation I turned on Web Server Logging, which logs all HTTP requests:</p>
<p><img class="aligncenter size-full wp-image-4641" src="{{ site.baseurl }}/assets/2014/09/azure-logging.jpg" alt="azure - logging" width="600" height="329" /></p>
<p>Then I found out this:</p>
<p><code>#Software: Microsoft Internet Information Services 8.0<br />
#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken<br />
2014-09-02 04:43:35 JJ09 POST /wp-login.php X-ARR-LOG-ID=f22e667c-3b13-4bdf-adf3-816cda8fa0db 80 - 195.211.154.159 Mozilla/4.0+(compatible;+MSIE+9.0;+Windows+NT+6.1;+125LA;+.NET+CLR+2.0.50727;+.NET+CLR+3.0.04506.648;+.NET+CLR+3.5.21022) - http://jj09.net/wp-login.php jj09.net 200 0 0 4573 787 624<br />
2014-09-02 04:43:36 JJ09 POST /wp-login.php X-ARR-LOG-ID=782db699-4467-418c-8814-7a8cb5ee7175 80 - 195.211.154.159 Mozilla/4.0+(compatible;+MSIE+9.0;+Windows+NT+6.1;+125LA;+.NET+CLR+2.0.50727;+.NET+CLR+3.0.04506.648;+.NET+CLR+3.5.21022) - http://jj09.net/wp-login.php jj09.net 200 0 0 4573 790 656<br />
2014-09-02 04:43:37 JJ09 POST /wp-login.php X-ARR-LOG-ID=79cb788b-d646-43d7-8012-c31d507557bf 80 - 195.211.154.159 Mozilla/4.0+(compatible;+MSIE+9.0;+Windows+NT+6.1;+125LA;+.NET+CLR+2.0.50727;+.NET+CLR+3.0.04506.648;+.NET+CLR+3.5.21022) - http://jj09.net/wp-login.php jj09.net 200 0 0 4573 788 1718<br />
2014-09-02 04:43:38 JJ09 POST /wp-login.php X-ARR-LOG-ID=7cc0286e-6b81-4802-851b-d5aaea20daf3 80 - 195.211.154.159 Mozilla/4.0+(compatible;+MSIE+9.0;+Windows+NT+6.1;+125LA;+.NET+CLR+2.0.50727;+.NET+CLR+3.0.04506.648;+.NET+CLR+3.5.21022) - http://jj09.net/wp-login.php jj09.net 200 0 0 4573 790 703<br />
2014-09-02 04:43:40 JJ09 POST /wp-login.php X-ARR-LOG-ID=29c99e85-4552-49c3-8527-290a3c68ac86 80 - 195.211.154.159 Mozilla/4.0+(compatible;+MSIE+9.0;+Windows+NT+6.1;+125LA;+.NET+CLR+2.0.50727;+.NET+CLR+3.0.04506.648;+.NET+CLR+3.5.21022) - http://jj09.net/wp-login.php jj09.net 200 0 0 4573 787 718<br />
2014-09-02 04:43:41 JJ09 POST /wp-login.php X-ARR-LOG-ID=49e52af5-b40e-406b-b64b-c80bc8cc6501 80 - 195.211.154.159 Mozilla/4.0+(compatible;+MSIE+9.0;+Windows+NT+6.1;+125LA;+.NET+CLR+2.0.50727;+.NET+CLR+3.0.04506.648;+.NET+CLR+3.5.21022) - http://jj09.net/wp-login.php jj09.net 200 0 0 4573 787 718<br />
2014-09-02 04:43:42 JJ09 POST /wp-login.php X-ARR-LOG-ID=d40f4c89-932f-4a81-bfc6-cd403ab8b71b 80 - 195.211.154.159 Mozilla/4.0+(compatible;+MSIE+9.0;+Windows+NT+6.1;+125LA;+.NET+CLR+2.0.50727;+.NET+CLR+3.0.04506.648;+.NET+CLR+3.5.21022) - http://jj09.net/wp-login.php jj09.net 200 0 0 4573 788 671<br />
2014-09-02 04:43:43 JJ09 POST /wp-login.php X-ARR-LOG-ID=7ec01966-00de-47d1-ab35-5fae51898269 80 - 195.211.154.159 Mozilla/4.0+(compatible;+MSIE+9.0;+Windows+NT+6.1;+125LA;+.NET+CLR+2.0.50727;+.NET+CLR+3.0.04506.648;+.NET+CLR+3.5.21022) - http://jj09.net/wp-login.php jj09.net 200 0 0 4573 787 703</code></p>
<p>Raw, POST requests to wp-login.php page from the same IP address (195.211.154.159) in every 1-2 seconds!</p>
<p>Looks like brute force attack. I checked this IP on <a href="http://www.abuseipdb.com/">AbuseIPDB</a>. It was repored once:</p>
<p><img class="aligncenter size-full wp-image-4671" src="{{ site.baseurl }}/assets/2014/09/hacker_ip.jpg" alt="hacker ip" width="408" height="286" /></p>
<p>I also check this IP with <a href="http://www.iptrackeronline.com/">ipTRACKERonline</a>:</p>
<p><img class="aligncenter size-full wp-image-4681" src="{{ site.baseurl }}/assets/2014/09/hacker_ip-tracking.jpg" alt="hacker ip - tracking" width="552" height="595" /></p>
<p>Looks like "the hacker" is working from underground!</p>
<p>It is even more interesting how "the attack" stopped:</p>
<p><code>2014-09-02 04:49:04 JJ09 POST /wp-login.php X-ARR-LOG-ID=d56af862-6675-4d63-aa1e-c5858b222467 80 - 195.211.154.159 Mozilla/4.0+(compatible;+MSIE+9.0;+Windows+NT+6.1;+125LA;+.NET+CLR+2.0.50727;+.NET+CLR+3.0.04506.648;+.NET+CLR+3.5.21022) - http://jj09.net/wp-login.php jj09.net 200 0 0 4579 787 658<br />
2014-09-02 04:49:05 JJ09 POST /wp-login.php X-ARR-LOG-ID=c63c5285-f667-4b49-a9ca-e6dc6c4a881d 80 - 195.211.154.159 Mozilla/4.0+(compatible;+MSIE+9.0;+Windows+NT+6.1;+125LA;+.NET+CLR+2.0.50727;+.NET+CLR+3.0.04506.648;+.NET+CLR+3.5.21022) - http://jj09.net/wp-login.php jj09.net 200 0 0 4579 790 718<br />
2014-09-02 04:49:06 JJ09 POST /wp-login.php X-ARR-LOG-ID=820525bb-5972-48d7-b873-e5143f07de60 80 - 195.211.154.159 Mozilla/4.0+(compatible;+MSIE+9.0;+Windows+NT+6.1;+125LA;+.NET+CLR+2.0.50727;+.NET+CLR+3.0.04506.648;+.NET+CLR+3.5.21022) - http://jj09.net/wp-login.php jj09.net 200 0 0 4579 789 1721<br />
2014-09-02 04:49:21 JJ09 GET / X-ARR-LOG-ID=60ce7301-6f46-4397-a24d-9afda6fe2f62 80 - 137.117.234.219 - - - jedryszek.com 200 0 0 134454 753 1562<br />
2014-09-02 04:50:56 JJ09 GET /sending-email-from-rails-application/&amp;sa=U&amp;ei=5EUFVLr8OYvIgwSntoGABQ&amp;ved=0CNsCEBYwVg&amp;usg=AFQjCNFrPOjfBT525UoKx41tEt5C4PeHYw/xmlrpc.php X-ARR-LOG-ID=2a586af6-67f9-41e3-90fe-3d21deeb545b 80 - 91.205.75.136 Mozilla/5.0+(Windows+NT+5.1;+rv:24.0)+Gecko/20100101+Firefox/24.0 - - jj09.net 404 0 0 93650 839 1407<br />
2014-09-02 04:52:02 JJ09 GET /wp-admin X-ARR-LOG-ID=8feceffd-e44d-4002-b66b-53c9d5ec354e 80 - 24.22.164.96 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit... - jj09.net 301 0 0 570 1540 31</code></p>
<p>First 3 requests are from "the hacker". Next one is a request from Azure Scheduler (I was testing Azure Scheduler to ping my blog every 5 mins). Then somebody visited my post about <a href="http://jj09.net/sending-email-from-rails-application/">Sending e-mail from Rails application</a>. The last one, is me logging on.</p>
<p>The standard hosting provider will probably require me to send an email asking about logs, and they probably will not have all logs...but on Azure I could just turn it on and check whatever I wanted. This shows the real power of the Cloud!</p>
<p>After this incident I installed <a href="https://bruteprotect.com/">BruteProtect</a> plug-in. It claims that since yesterday it blocked 65 attacks on my blog:</p>
<p><img class="aligncenter size-full wp-image-4741" src="{{ site.baseurl }}/assets/2014/09/brute-protect1.jpg" alt="BruteProtect" width="400" height="471" /></p>
<p>To be honest. I was shocked. I assumed that some attacks happened in the past, but 65 in 1 days? No idea if it is true, but I will give it a try and see what will happen in a week or a month.</p>
<p>Did you have attacks on your blogs/websites? What kind? How did you find out? What did you do to stop it and prevent in the future?</p>

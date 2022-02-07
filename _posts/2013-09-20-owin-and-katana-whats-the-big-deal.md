---
layout: post
title: OWIN and Katana - what's the big deal?
date: 2013-09-20 00:14:11.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- ".NET"
- asp.net
- C#
- Katana
- Open Source
- OWIN
meta:
  _yoast_wpseo_linkdex: '62'
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _yoast_wpseo_focuskw: owin katana tutorial
  _syntaxhighlighter_encoded: '1'
  dsq_thread_id: '1779665331'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/owin-and-katana-whats-the-big-deal/"
---
<p>OWIN stands for The <strong>O</strong>pen <strong>W</strong>eb <strong>I</strong>nterface for .<strong>N</strong>ET. It is a standard for communication between .NET web servers and web applications. It defines required elements for HTTP request (<a href="http://owin.org/spec/owin-1.0.0.html#_3._Request_Execution">details</a>). It is inspired by <a href="http://rack.github.io/">Rack</a> from Ruby on Rails World. Katana is implementation of this standard. We can say that it is a lightweight web server for .NET. In fact, it is more than that (more info <a href="http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana">here</a>).</p>
<h4>Demo</h4>
<p>First, we need to create application project. Let's create 'Empty Web Application' (it might be also Console App).</p>
<p><img src="{{ site.baseurl }}/assets/2013/09/owin-emptyProj.jpg" alt="OWIN - empty Project" width="100%" class="aligncenter size-full wp-image-674" /></p>
<p>Next, we will install two NuGet packages (using Package Manager Console):</p>
<p><code>Install-Package Microsoft.Owin.Host.SystemWeb</code></p>
<p><code>Install-Package Owin.Extensions</code></p>
<p>Then, we need to create 'Startup class'.</p>
{% highlight csharp %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using Owin;

namespace OwinDemo
{
    public class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            app.UseHandlerAsync((req, res) =>
            {
                res.ContentType = "text/plain";
                return res.WriteAsync('Hello Katana!");
            });
        }
    }
}
{% endhighlight %}
<p>Now we are ready to run our web server, but you may get following error:</p>
<p><img src="{{ site.baseurl }}/assets/2013/09/owin-error.jpg" alt="OWIN - error" width="518" height="71" class="aligncenter size-full wp-image-677" /></p>
<p>Fortunately there is easy fix for that. You need to modify Web.config file, adding following code in <em>configuration </em>section:</p>
{% highlight xml %}
<appSettings>
    <add key="owin:HandleAllRequests" value="true"/>
</appSettings>
{% endhighlight %}

<p>Then you can run server (CTRL+F5) and you should see:</p>
<p><img src="{{ site.baseurl }}/assets/2013/09/owin-helloKatana.jpg" alt="OWIN - Hello Katana" width="135" height="53" class="aligncenter size-full wp-image-681" /></p>
<h4>Summary</h4>
<p>So, what is big deal? We have web server in 7 lines of code! We do not need IIS as only one, right choice.</p>
<p>Of course we can do much more sophisticated things. Such as routing, WebAPI or even SignalR. You can also debug it easily. </p>
<p>More info about OWIN and Katana on ASP.NET website: <a href="http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana">An Overview of Project Katana</a><br />
There is also screencast on Channel9: <a href="http://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET">The Katana Project - OWIN for ASP.NET</a> (it shows e.g. how to use WebAPI from 35:40).<br />
<a href="http://www.dotnetcurry.com/ShowArticle.aspx?ID=915">Here</a> is very nice article how to use SignalR with Katana.</p>
<p>Katana is Open Source and available on <a href="http://katanaproject.codeplex.com/">CodePlex</a>. </p>

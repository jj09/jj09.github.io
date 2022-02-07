---
layout: post
title: Windows PowerShell profile
date: 2013-11-06 13:41:25.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- tools
tags:
- PowerShell
- terminal
- windows
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _syntaxhighlighter_encoded: '1'
  dsq_thread_id: '1942437823'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/windows-powershell-profile/"
---
<p>Windows PowerShell is very powerful tool. It contains <a href="http://ss64.com/ps/">many useful commands</a>. One of my favorite features is possibility to use some well-known bash commands such as: <em>ls</em> or <em>pwd</em>, which are missing in Windows Command Prompt. The cool thing is the fact, that PowerShell contains combination of Windows Command Prompt and Bash shell commands. E.g. for copying you can use <em>copy</em> (Windows) and <em>cp</em> (Bash). </p>
<p>You can also have personal configuration file (like .bashrc in Unix) to set some persistent settings. To find out, where it is located use command:</p>

{% highlight console %}
PS C:\> echo $PROFILE
C:\Users\jj09\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
{% endhighlight %}

<p>I needed to create directory 'WindowsPowerShell' and profile file before adding some custom settings. Additionally, I needed to enable scripts on my system (it is disabled by default).</p>

{% highlight console %}
PS C:\> Set-ExecutionPolicy RemoteSigned
{% endhighlight %}

<p>More info about Execution Policies can be found <a href="http://technet.microsoft.com/en-us/library/ee176949.aspx">here</a>.</p>
<p>My Microsoft.PowerShell_profile.ps1 file:</p>
{% highlight console %}
set-alias subl "C:\Program Files\Sublime Text 2\sublime_text.exe"
set-alias grep select-string
set-alias ssh New-PSSecureRemoteSession
set-alias sh New-PSRemoteSession
set-alias l ls
{% endhighlight %}
<p>There is also 'Power' version of PowerShell called ISE (Integrated Scripting Environment). Be aware, that it has different profile file (for me it is: <em>C:\Users\jj09\Documents\WindowsPowerShell\Microsoft.PowerShellISE_profile.ps1</em>). You can check it with the same command like for standard PowerShell (<em>echo $PROFILE</em>). <a href="http://4sysops.com/archives/10-reasons-for-using-powershell-ise-instead-of-the-powershell-console/">Here</a> is a list of top 10 killer features, which are in ISE, but not in standard PS (Intellisense is my favorite).</p>
<p><img src="{{ site.baseurl }}/assets/2013/11/PowerShell-autocomplete.jpg" alt="PowerShell-autocomplete" width="669" height="261" class="aligncenter size-full wp-image-778" /></p>
<p>Disadvantage of PowerShell is its loading time. Windows Command prompt loads instantaneously, but PS need ~1 second. It is even worse in case of ISE, which needs ~3 seconds (on my Thinkpad X220: i5/8GB/SSD).</p>
<p>You can add custom configuration to Windows Command Prompt too. To do that you need to <a href="http://devblog.point2.com/2010/05/14/setup-persistent-aliases-macros-in-windows-command-prompt-cmd-exe-using-doskey/">run command prompt with some arguments</a>.</p>

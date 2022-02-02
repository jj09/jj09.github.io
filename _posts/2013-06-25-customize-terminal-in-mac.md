---
layout: post
title: Customize Terminal in Mac
date: 2013-06-25 09:15:21.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- tools
tags:
- iterm
- macbook
- macos
- terminal
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
  dsq_thread_id: '1505346170'
  feature_size: blank
  builder_switch_frontend: '0'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/customize-terminal-in-mac/"
---
<p>Mac (UNIX) users use to be working with Terminal a lot. There is a few tips, which can make your life easier. First of all, if you are working on Mac - install <a href="http://www.iterm2.com/">iTerm2</a> and use it instead of standard Terminal. It is just more powerful. There is many <a href="http://www.iterm2.com/#/section/features">features</a> not available in standard Terminal. I find very useful the possibilities to search with CMD+F and copy entire path with double click by mouse (when you double click in standard Terminal it copies only one word). Another cool thing is 'split terminal' view. You can have multiple panes in one window.<br />
<img class="aligncenter size-full wp-image-6931" src="{{ site.baseurl }}/assets/2013/06/iTerm2-multipane1.png" alt="iTerm2 - multipane" width="853" height="486" /></p>
<p>Second improvement to work faster is creation some aliases for commonly use commands. E.g. <em>ls</em>, <em>clear</em> or <em>la -ls</em>. You might also want to customize command prompt. I don't like the standard one with Machine and user name (I always know in which Machine I am, and which user I am using - in case of doubts I can use <em>whoami</em>). To do add aliases and change default command prompt you need to modify your ~/.bashrc file. There is my .bashrc:</p>
<p>[bash]alias dir='ls -lap'<br />
alias l='ls'<br />
alias p='pwd'<br />
alias c='clear'<br />
alias o='open'<br />
alias tree=&quot;ls -R | grep \&quot;:$\&quot; | sed -e 's/:$//' -e 's/[^-][^\/]*\//--/g' -e '\s/^/   /' -e 's/-/|/'&quot;<br />
export PS1=&quot;[\W]$ &quot;[/bash]</p>
<p><a href="http://www.cyberciti.biz/tips/howto-linux-unix-bash-shell-setup-prompt.html">Here</a> you can find a list of various options to customize your command prompt.</p>
<p>To load this settings automatically each time you run Terminal, you also need to add below command to ~/.profile file:</p>
<p><code>source ~/.bashrc</code></p>
<p>After above improvements my terminal looks like that:</p>
<p><img class="aligncenter size-full wp-image-195" src="{{ site.baseurl }}/assets/2013/06/iTerm2.png" alt="iTerm2" width="600px" /></p>
<p>Hint: when you are playing with your command prompt (or aliases), you can simple run command <em>source ~/.bashrc</em> from terminal to check the result of changes you made.</p>
<p>And of course I use black terminal with green font color.</p>
<p><img class="alignnone size-full wp-image-256" src="{{ site.baseurl }}/assets/2013/06/We-are-Hackers.png" alt="We are Hackers" width="400" height="164" /></p>

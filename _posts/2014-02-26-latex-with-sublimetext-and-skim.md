---
layout: post
title: LaTeX with SublimeText and Skim
date: 2014-02-26 22:04:12.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- tools
tags:
- LaTeX
- SublimeText
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  dsq_thread_id: '2328043863'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/latex-with-sublimetext-and-skim/"
---
<p><img src="{{ site.baseurl }}/assets/2014/02/SublimeText-LaTeXTools-785x577.png" alt="SublimeText with LaTeX Tools plugin" width="785" height="577" class="aligncenter size-large wp-image-1041" /></p>
<p>Recently I started writing my Master Thesis. I decided I will do it in LaTeX. </p>
<p>I work most of the time on MacBook. The most popular LaTeX distribution for Mac is <a href="http://tug.org/mactex/">MacTeX</a> (for Windows: <a href="http://miktex.org/">MiKTeX</a> or <a href="https://www.tug.org/texlive/">TeXlive</a>). Once I had this installed I needed editor. First I was using <a href="https://www.tug.org/texworks/">TeXworks</a>, but it is not very decent environment. Nice thing about it is the built-in PDF viewer. Every time I rebuild the document it refresh generated pdf. However, it's hard to manage documents with more than one .tex file. My Master Thesis consists multiple files and I end up editing files in SublimeText and building pdf with TeXworks. Not cool!</p>
<p>Today, one friend of mine showed me application, which detects .pdf updates automatically: <a href="http://skim-app.sourceforge.net/">Skim</a>. I have also found <a href="https://github.com/SublimeText/LaTeXTools">LaTeXTools</a> plugin for SublimeText. It allows to build .tex document with CMD+B (Mac) or CTRL+B (Windows/Linux). Moreover, Skim can be integrated with SublimeText in such a way that it checks for updates every time, you perform build in SublimeText.</p>
<h3>LaTeX + SublimeText + Skim setup</h3>
<ol>
<li>Install LaTeX distribution (for Mac OS X: <a href="http://tug.org/mactex/">MacTeX</a>, for Windows: <a href="http://miktex.org/">MiKTeX</a> or <a href="https://www.tug.org/texlive/">TeXlive</a>).</li>
<li>Install <a href="http://www.sublimetext.com/3">SublimeText</a>
<ul>
<li>Optionally: Install <a href="http://wbond.net/sublime_packages/package_control">SublimeText Package Control</a> (if you didn't do that already) - it will be easier to install LaTeXTools package.</li>
</ul>
</li>
<li>Install <a href="https://github.com/SublimeText/LaTeXTools">LaTeXTools</a> plugin. With <a href="http://wbond.net/sublime_packages/package_control">SublimeText Package Control</a> installed: click CMD+SHIFT+P (on Mac) or CTRL+SHIFT+P (Win/Linux). More details can be found <a href="https://github.com/SublimeText/LaTeXTools">here</a>.
<ul>
<li>Mac users: You may need to install 'latexmk': <code>sudo tlmgr install latexmk</code> (more info can be found in <a href="https://github.com/SublimeText/LaTeXTools/blob/master/README.markdown">LaTeXTools README</a>).</li>
</ul>
</li>
<li>Install <a href="http://skim-app.sourceforge.net/">Skim</a> (for Windows users: check <a href="http://blog.kowalczyk.info/software/sumatrapdf/download-free-pdf-viewer.html">Sumatra PDF</a>).</li>
<li>In Skim: go to Preferences->Sync and set 'preset' to SublimeText.</li>
</ol>
<p><img src="{{ site.baseurl }}/assets/2014/02/Skim-preferences.png" alt="Skim preferences" width="507" height="317" class="aligncenter size-full wp-image-1037" /></p>
<p>After that you just need to build LaTeX document in SublimeText with CMD+B (Mac) or CTRL+B (Win/Linux). Open the generated .pdf in Skim, then every time you rebuild it in SublimeText - it will be refreshed automatically.</p>
<p>If you have multiple documents add <code>%!TEX root = &lt;master file name&gt;</code> at the beginning of every file.</p>
<p>It is much more convenient than using SublimeText and TeXworks for rebuilding pdf. Additionally, TeXworks' PDF viewer is not very decent.</p>
<p>For LaTeX editing, I have found also <a href="http://texstudio.sourceforge.net/">TeXstudio</a>. It looks good, but I didn't test it so far.</p>

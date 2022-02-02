---
layout: post
title: Gulp - tutorial
date: 2014-11-13 20:36:09.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- gulp
- javascript
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
  dsq_thread_id: '3222860813'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/gulp-tutorial/"
---
<p><img class="aligncenter size-full wp-image-6561" src="{{ site.baseurl }}/assets/2014/11/gulpjs.png" alt="gulp.js" width="134" height="271" /></p>
<p>Gulp is a streaming build system (aka task runner). It contains plugins, which allows you to run tasks such as TypeScript to JavaScript compilation, Less to CSS compilation, bundling, minification, running you own scripts, and much, much more.</p>
<h3>Installation</h3>
<p>Required: <a href="https://www.npmjs.org/">npm</a> (Node Packaged Modules). You can install it with <a href="https://chocolatey.org/">Chocolatey</a>:</p>
<p><code>cinst nodejs</code></p>
<p>When you have npm, you are good to go and install Gulp:</p>
<p><code>npm install -g gulp</code></p>
<p>After installation, localize "gulp.cmd" file, and add its location to your PATH. Location depends on the way how you installed nodejs. On my one machine, where I installed nodejs using the <a href="http://nodejs.org/download/">installer</a>, it is in C:\Users\jjed\AppData\Roaming\npm directory. On my other machine, where I installed nodejs from Chocolatey, it is in C:\ProgramData\chocolatey\lib\nodejs.commandline.0.10.31\tools. I recommend you <a href="http://www.voidtools.com/">Everything Search Engine</a> not only for this task, but for searching all kind of files on your machine. It is ridiculously fast, and when you pin it to your task bar as the first item, you can invoke it with WIN+1.</p>
<p>I wish npm installation did this work (adding gulp to PATH) automatically.</p>
<h3>Gulp Hello World</h3>
<p>Open the Console (I recommend <a href="http://sourceforge.net/projects/conemu/">ConEmu</a> as you Console on Windows), and cd into your project directory (for now it can be even empty directory).</p>
<p>From your project root directory run:</p>
<p><code>npm install --save-dev gulp</code></p>
<p>Create <em>gulpfile.js</em> file in the root of your project:</p>
{% highlight javascript %}var gulp = require('gulp');

gulp.task('default', function () {
  console.log("Hello, world!");
});
{% endhighlight %}
<p>Run gulp:</p>
<p><code>gulp</code></p>
<p>You should see the following result (with different time stamps and path, probably):</p>
<p><code>[21:45:32] Using gulpfile C:\dev\myproj\gulpfile.js<br />
[21:45:32] Starting 'default'...<br />
Hello, world!<br />
[21:45:32] Finished 'default' after 141 µs</code></p>
<p>The default task is invoked when you run gulp.js without any arguments. You can run other tasks from <code>default</code> task. Below file contains <code>hello</code> task, and invoke it from the <code>default</code> task:</p>
{% highlight javascript %}var gulp = require('gulp');

gulp.task('hello', function () {
  console.log("Hello, world!");
});

gulp.task('default', ['hello']);
{% endhighlight %}
<p>The result of gulp run is a little bit different now:</p>
<p><code>[21:49:21] Using gulpfile C:\dev\myproj\gulpfile.js<br />
[21:49:21] Starting 'hello'...<br />
Hello, world!<br />
[21:49:21] Finished 'hello' after 210 µs<br />
[21:49:21] Starting 'default'...<br />
[21:49:21] Finished 'default' after 8.21 µs</code></p>
<h3>Using Gulp to compile TypeScript files 'on change'</h3>
<p>Install TypeScript (if you do not have it installed already):</p>
<p><code>npm install -g typescript</code></p>
<p>Make sure <code>tsc</code> is in your path.</p>
<p>Install TypeScript compiler for gulp.js (from your project root directory):</p>
<p><code>npm install --save-dev gulp-tsc</code></p>
<p>Create <em>TypeScript</em> directory, and cd into it:</p>
<p><code>mkdir TypeScript<br />
cd TypeScript</code></p>
<p>Create simple <em>hello.ts</em> file:</p>
{% highlight javascript %}function greeter(person: string) {
    return "Hello, " + person;
}

var user = "Anders Hejlsberg";

console.log(greeter(user));
{% endhighlight %}
<p>Go to root directory of your project and create <em>js</em> directory (it will be output directory for generated JavaScript files):</p>
<p><code>mkdir js</code></p>
<p>Modify <em>gulpfile.js</em>:</p>
{% highlight javascript %}var gulp = require('gulp'),
	typescript = require('gulp-tsc');

gulp.task('typescript-compile', function(){
  return gulp.src(['TypeScript/*.ts'])
    .pipe(typescript())
    .pipe(gulp.dest('js/'));
});

gulp.task('watch', function () {
  gulp.watch('TypeScript/*.ts', ['typescript-compile']);
});

gulp.task('default', ['typescript-compile', 'watch']);
{% endhighlight %}
<p>Once you run gulp it will compile all TypeScript files from <em>TypeScript</em> directory to <em>js</em> directory. Furthermore, Gulp will not suspend, but it will watch all .ts files under TypeScript directory, and will recompile them every time you change and save some of them. Try it!</p>
<h3>Prevent gulp.js from crashing by handling errors</h3>
<p>You can notice that if some of your TypeScript files cause compilation error (e.g., because of syntax error) then gulp crashes.</p>
<p>In order to avoid it, you can add simple error handling function (<code>errorLog</code>) to <em>gulp.js</em> file, and call it in the <em>typescript-compile</em> task pipeline:</p>
{% highlight javascript %}var gulp = require('gulp'),
	typescript = require('gulp-tsc');

function errorLog (error) {
  console.error.bind(error);
  this.emit('end');
}

gulp.task('typescript-compile', function(){
  return gulp.src(['TypeScript/*.ts'])
    .pipe(typescript())
    .on('error', errorLog)
    .pipe(gulp.dest('js/'));
});

gulp.task('watch', function () {
  gulp.watch('TypeScript/*.ts', ['typescript-compile']);
});

gulp.task('default', ['typescript-compile', 'watch']);
{% endhighlight %}
<p>Now, Gulp will not crash, but display compilation error, and recompile files after next file change.</p>
<h3>Using gulp.js to run batch/bash script</h3>
<p>Let assume that you want to run some script (batch file on Windows, or bash script on Unix) after TypeScript files compilation.</p>
<p>First, we need to install <em>gulp-shell</em> plugin:</p>
<p><code>npm install gulp-shell</code></p>
<p>To keep it simple, our script will only output text <em>"TypeScript compilation done"</em> to the console.</p>
<p>Create file build.cmd in your project root directory:</p>
{% highlight batch %}echo "TypeScript compilation done"{% endhighlight %}
<p>And modify <em>gulpfile.js</em>:</p>
{% highlight javascript %}var gulp = require('gulp'),
  run = require('gulp-shell'),
  typescript = require('gulp-tsc');

function errorLog (error) {
  console.error.bind(error);
  this.emit('end');
}

gulp.task('typescript-compile', function(){
  return gulp.src(['TypeScript/*.ts'])
    .pipe(typescript())
    .on('error', errorLog)
    .pipe(gulp.dest('js/'))
    .pipe(shell(['build.cmd']));
});

gulp.task('watch', function () {
  gulp.watch('TypeScript/*.ts', ['typescript-compile']);
});

gulp.task('default', ['typescript-compile', 'watch']);{% endhighlight %}
<p>In real-life you may want to copy all compiled files to some other directory, or do some other "your project specific" task.</p>
<p>Using <em>gulp-shell</em> you can run any command, or set of commands (concatenating them with '<em>&amp;</em>' on Windows, or '<em>&amp;&amp;</em>' on Unix), e.g.:</p>
<p><code>shell(['cd c:/dev/myproj/src &amp; build']);</code></p>
<h3>Summary</h3>
<p>Gulp is very handful tool. However it is not the only one. Its main rival is <a href="http://gruntjs.com/">Grunt.js</a>. Actually, Gulp was inspired by Grunt. Most of people (based on my research) prefer Gulp over Grunt. Main argument: it allows to stream results (run multiple operations on set of files), and it is less verbose (allows to do more with less configuration). Check Grunt vs Gulp comparison in <a href="http://travismaynard.com/writing/no-need-to-grunt-take-a-gulp-of-fresh-air">this blog post</a>, and <a href="http://vimeo.com/97519516">this Steve Sanderson's talk</a> (starting from 30:50).</p>
<p>To get more of Gulp check <a href="http://travismaynard.com/writing/getting-started-with-gulp">Getting Started With Gulp</a>, <a href="https://www.youtube.com/watch?v=wNlEK8qrb0M&amp;list=PLLnpHn493BHE2RsdyUNpbiVn-cfuV7Fos">Learning Gulp</a>, and <a href="https://github.com/gulpjs/gulp/tree/master/docs">gulp documentation</a>.</p>
<p>Are you using Gulp or Grunt, or some other task runner?</p>
<p><b>EDIT</b>: I updated the post with <code>return</code> statements in tasks. This <a href="http://stackoverflow.com/questions/21699146/gulp-js-task-return-on-src">informs task system that particular task is async</a>, and prevents from occasional crashes when called from <em>watch</em> task.</p>

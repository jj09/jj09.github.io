---
layout: post
title: vim on Windows
date: 
type: post
parent_id: '0'
published: false
password: ''
status: draft
categories:
- tools
tags:
- IDE
- vim
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
  _oembed_8d90e4a27407703dbbddf5c429ffe675: <iframe width="500" height="375" src="https://www.youtube.com/embed/ITZleEWYoU8?feature=oembed"
    frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
  _oembed_time_8d90e4a27407703dbbddf5c429ffe675: '1534263521'
  _oembed_44601976016712eebb75b1fddaefa85b: '<blockquote class="wp-embedded-content"
    data-secret="gZP0hKSao8"><a href="https://n3wjack.net/2014/08/25/setting-up-vim-on-windows/">setting
    up vim on windows</a></blockquote><iframe class="wp-embedded-content" sandbox="allow-scripts"
    security="restricted" style="position: absolute; clip: rect(1px, 1px, 1px, 1px);"
    src="https://n3wjack.net/2014/08/25/setting-up-vim-on-windows/embed/#?secret=gZP0hKSao8"
    data-secret="gZP0hKSao8" width="500" height="282" title="&#8220;setting up vim
    on windows&#8221; &#8212; n3wjack&#039;s blog" frameborder="0" marginwidth="0"
    marginheight="0" scrolling="no"></iframe>'
  _oembed_95ab6ced16de916498c39d5a645a3174: "{{unknown}}"
  _oembed_d69b5605512f79a8a5ea0b1f8b64707b: "{{unknown}}"
  _oembed_5215ba62395046433482f6fb343d2462: "{{unknown}}"
  _oembed_a304aa6c8c6fc9aa0823662069ce0566: "{{unknown}}"
  _oembed_fa3493e189963471f0d9d0d0cea03dd7: "{{unknown}}"
  _oembed_1426686cb06fc389fe00e795ed75f798: "{{unknown}}"
  _oembed_1dfc91e2e0cd36eb2fc3b153bc710976: "{{unknown}}"
  _oembed_39673e77fd666a8e8b77bed182dc3795: "{{unknown}}"
  _oembed_be80b940b5fd290359bc9e5dea551b41: "{{unknown}}"
  _oembed_5d9486bc22d4ec4b246025b317a2efe6: "{{unknown}}"
  _oembed_bea8e64c3654ed840d241e26ac9c2403: "{{unknown}}"
  _oembed_748eb13096016b523a7d9e1eff28342c: "{{unknown}}"
  _oembed_time_44601976016712eebb75b1fddaefa85b: '1534263525'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/"
---
<p>Basic Setup</p>
<p>install vim (c:/vim is the best): http://www.vim.org/download.php#pc</p>
<p>install pathogen: http://www.vim.org/scripts/script.php?script_id=2332 (unzip pathogen.vim to c:/vim/vimfiles/autoload/pathogen.vim)</p>
<p>create c:/Users/jjed/_vimrc file<br />
https://amix.dk/vim/vimrc.html<br />
https://github.com/amix/vimrc</p>
<p>- create directories: backups, swaps in c:/vim/vimfiles</p>
<p>install NERDTree:<br />
cd c:/vim/vimfiles/bundle<br />
git clone https://github.com/scrooloose/nerdtree.git</p>
<p>download some cool color theme: http://www.vim.org/scripts/script_search_results.php?keywords=&amp;script_type=color+scheme&amp;order_by=downloads&amp;direction=descending&amp;search=search</p>
<p>Web Developer plugins<br />
http://gosukiwi.svbtle.com/vim-configuration-for-web-development</p>
<p>TypeScript plugins</p>
<p>links:</p>
<p>https://www.youtube.com/watch?v=ITZleEWYoU8<br />
http://n3wjack.net/2014/08/25/setting-up-vim-on-windows/<br />
http://www.vim.org/ugrankar.pdf<br />
http://usevim.com/2012/10/12/vim101-windows/<br />
https://github.com/leafgarland/typescript-vim</p>
<p>&nbsp;</p>
<p>getting started:</p>
<p>http://yehudakatz.com/2010/07/29/everyone-who-tried-to-convince-me-to-use-vim-was-wrong/</p>
<p>http://www.viemu.com/a-why-vi-vim.html</p>
<p>&nbsp;</p>
<p>vim as default git editor - git updates are messing it up, overwriting paths to vim (solution: cp/paste after updates)</p>

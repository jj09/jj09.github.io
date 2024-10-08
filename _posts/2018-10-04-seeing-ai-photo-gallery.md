---
layout: post
title: Seeing AI Photo Gallery
date: 2018-10-04 21:03:35.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- ios
- SeeingAI
- Xamarin
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
  dsq_thread_id: '6950965302'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/seeing-ai-photo-gallery/"
---
<p><img class="aligncenter size-full wp-image-19664" src="{{ site.baseurl }}/assets/2018/10/Microsoft-Seeing-AI.png" alt="Microsoft Seeing AI" width="900" height="450" /></p>
<p>Seeing AI is a mobile app that narrates the world around you. It enables people with low vision to recognize faces, objects, text, bills, colors, and much more! Seeing AI was first announced at <a href="https://www.youtube.com/watch?v=rVF2duPVUTY">//build conference in 2016</a>.</p>
<p>Over last few months I was working with Seeing AI team overnight on in-app Photo Gallery that allows you to browse through photos that you have taken earlier. Before you could only take photo, analyze it, and save (without description). Now, you can save it with description that you can later retrieve. You can also analyze photos taken with your phone camera.</p>
<p><iframe src="https://www.youtube.com/embed/tsQMkKCnr9Q?ecver=1" width="855" height="481" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>One of the challenges was to decide what details about the photo should we present. We have a lot of different channels (short text, document, person, scene, etc.). For now we decided to show scene description, place and date when photo was taken. Let us know if you have suggestions to improve this!</p>
<p><img class="aligncenter size-full wp-image-19661" src="{{ site.baseurl }}/assets/2018/10/SeeingAI-photogallery-e1538709662987.png" alt="SeeingAI - photo gallery" width="400" height="711" /></p>
<p>Another problematic part was deciding how to distinguish between analyzed, and not analyzed photos. Initially we had a toggle to switch between recognized photos and all photos. Ultimately we decided to have only 1 view with all photos. Thoughts?</p>
<p>For non recognized photos we needed to provide mechanism to analyze them. Initially user had to open photo, and explicitly tap 'analyze'. We changed this approach to automatically analyze not recognized photos when going to full screen view, and enable users to reanalyze them. The 'reanalyze' button might be useful in situations where we update app with new AI models. These models may do better job in recognizing photos.</p>
<p>Seeing AI is built with Xamarin iOS native. I was surprised that we had to build entire gallery from scratch. There was no plugin or open source sample we could use. Hint: opportunity for you!</p>
<p>You can download Seeing AI from <a href="https://itunes.apple.com/us/app/seeing-ai/id999062298?mt=8">App Store</a>.</p>

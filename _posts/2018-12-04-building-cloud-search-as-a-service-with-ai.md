---
layout: post
title: Building Cloud Search as a Service with AI
date: 2018-12-04 09:43:01.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- career
tags:
- AI
- Azure
- AzureSearch
- Cognitive Search
- JFK files
- machine learning
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
  dsq_thread_id: '7087292812'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/building-cloud-search-as-a-service-with-ai/"
---
<p><img class="aligncenter size-full wp-image-19688" src="{{ site.baseurl }}/assets/2018/12/ai-search.jpg" alt="AI Search" width="800" height="450" /></p>
<p>It's been almost a year since <a href="https://jj09.net/i-am-joining-cloud-ai-team-to-work-on-azure-search/">I joined Azure Search team</a>. A lot has changed since then. I joined right after team doubled by merge with Text Analytics team with a mission to add intelligence to search. A few months later entire Cognitive Services (Azure Machine Learning APIs) platform team joined us. Then we hired additional developers to build scalable platform for both Cognitive Services and Azure Search. After that we also got a team of data scientists who are building the actual machine learning models. Now, as the Applied AI team, we are in the center of AI and Cloud at Microsoft.</p>
<p>Azure Search is a search-as-a-service cloud solution that gives developers APIs and tools for adding a rich search experience in web and mobile applications. You get for free things like autocomplete, suggestions, synonyms, results highlighting, facets, filters, sorting and paging. Functionality is exposed through <a href="https://docs.microsoft.com/rest/api/searchservice/">REST API</a> or <a href="https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk">.NET SDK</a>. The biggest pain, which is infrastructure and availability are managed by us.</p>
<p><!--I am with the team almost a year. One of the first things I did was to build website that demonstrates capabilities of our service, which was used in a meeting with Satya and a CEO of "a big company that everybody knows". We imported large data set into search index, and using <a href="https://github.com/jj09/AzSearch.js">AzSearch.js</a> we built Single Page App that allowed to search through it with autocomplete, suggestions and spellchecks. Thanks to Azure Search backend we got all that stuff for free. The only thing we needed to do was to create Search service, and import data into the search index. The search results ranking and precision was pretty good not only thanks to internal capabilities that you get for free (distance search, etc.), but also thanks to <a href="https://docs.microsoft.com/en-us/azure/search/search-synonyms">synonym maps</a> that we added. Both Satya and "the CEO" liked it.</p>
<p>After demoing all of these for Satya, we improved this demo and showed it to Harry Shum (Executive VP of AI and Research Group at Microsoft). Again, demo was well received and it led to double-down on investing into making Azure Search even smarter. How can you do that? The answer is obvious. Use AI. But how? By enabling developers to take advantage of machine learning seamlessly without worrying about implementation details. We were already doing this, but we came up with a few more ideas that you will hear about in near future when we ship them :)--></p>
<p>While having all of that, we also need a great developer experience. Everybody needs to be able to understand how to build that Search AI pipeline without spending hours on reading docs. This is another thing we are working on. Email me or <a href="https://twitter.com/realJacobJed">tweet message</a> me if you are interested in that kind of stuff.</p>
<h3>Where are we going?</h3>
<p><img class="aligncenter size-full wp-image-19560" src="{{ site.baseurl }}/assets/2018/12/grok-overview.png" alt="Cognitive Search" width="721" height="355" /></p>
<p>We want to build the best Search as a Service platform that enables developers to add <del datetime="2018-11-29T18:42:42+00:00">Bing-like</del> Google-like search experience to their websites. No need for hiring search experts who know what inverted index is. No challenges with shard allocation and how to implement master election properly. No need for distributed systems expertise to scale this for large amount of data. Last, but not least: no need for setting up, owning and managing the infrastructure. Everything is being taken care of by the platform. By the Cloud.</p>
<p>Our team is also working on <a href="https://www.altexsoft.com/blog/datascience/comparing-machine-learning-as-a-service-amazon-microsoft-azure-google-cloud-ai-ibm-watson/">market-leading Machine Learning APIs</a>. We are going to utilize these ML models and enable you to search through not only text, but also through your images, audio and videos.</p>
<p>There is a lot of challenges in that journey. From processing large amounts of data, through doing it in reasonable time (performance/parallelization), to providing efficient user experience throughout the process.</p>
<h3>Where are we now?</h3>
<p>We already have fast, reliable and production-ready system for full-text search. You can provision it in no-time, scale by adding more replicas or partitions, and monitor using metrics we provide. You can query it with .NET SDK or using REST API. We even have Open Source UI generation tool that gets you started with the latter: <a href="https://github.com/jj09/AzSearch.js">AzSearch.js</a>.</p>
<p>To learn more about current capabilities of Azure Search check this awesome presentation by <a href="https://twitter.com/bryan_soltis">Bryan Soltis</a>:</p>
<p><iframe src="https://www.youtube.com/embed/C1k0MG9G6Cw?ecver=1" width="640" height="360" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>There are two ways to populate your search index: by simply inserting documents (records) into it, or by using <a href="https://docs.microsoft.com/en-us/azure/search/search-indexer-overview">indexer</a> - a mechanism that enables you to sync your search index with your data source (SQL or NoSQL Database, blob storage, etc.).</p>
<p>We have already started adding AI to our search pipeline, by enabling you to run text analytics and OCR on your data. If you are using <a href="https://docs.microsoft.com/en-us/azure/search/search-indexer-overview">indexer</a>, you can create a <a href="https://docs.microsoft.com/en-us/azure/search/cognitive-search-defining-skillset">skillset</a>, which can detect people, entities, organizations, locations, key phrases, and language on the textual data. On top of that you can use OCR that can recognize text from your images, and enable you to search through that text. You can also run mentioned text analytics on recognized text. We call this approach <a href="https://jj09.net/cognitive-search-azure-search-with-ai/">Cognitive Search</a>. Here is a quick video by Brian and Corom from our team, with a sneak peak of what's possible:</p>
<p><iframe src="https://www.youtube.com/embed/XRI0DnjAgmo?ecver=1" width="640" height="360" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>Last year we created a prototype of Cognitive Search, using JFK files that went public. You can check out our <a href="https://jfkfiles2.azurewebsites.net/">JFK files website</a>, <a href="https://github.com/Microsoft/AzureSearch_JFK_Files">github repo</a> and below video from Connect(); conference in 2017, where Corom explaines how he built a pipeline to achieve what is possible now with just checking the checkbox:</p>
<p><iframe src="https://www.youtube.com/embed/JFdF-Z7ypQo?ecver=1" width="640" height="360" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>We announced Cognitive Search at the //build conference earlier this year. Together with NBA we built a website that allows you to search through player's photos. You can search for players, their shoes or correlations between them:</p>
<p><iframe src="https://www.youtube.com/embed/8i4snWofThk?ecver=1" width="640" height="360" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>Similar approach can be used for variety of different scenarios. From filtering your family photos, through analyzing medical records data, to deciding <a href="https://youtu.be/Gzwq6JC6qwY?t=428">which crypto-currency to buy</a>. Now, all these PDFs and doc documents you have on your hard drive can be used to make an informed business decision.</p>
<p>There are a lot of companies using Azure Search in production. It's super exciting for me that <a href="https://customers.microsoft.com/en-us/story/real-madrid">Real Madrid is using Azure Search</a>. It's my favorite football club since I was a kid.</p>
<h3>How's the team?</h3>
<p>My favorite thing about our team are the people. Every single person is bringing something else to the table, and there is something you can learn from each one of them. From distributed systems expertise, through API design, to building efficient monitoring infrastructure that enables to maintain production cloud service. One of our team members is <a href="https://en.wikipedia.org/wiki/Henrik_Frystyk_Nielsen">Henrik Frystyk Nielsen</a> who is best known for his pioneering work on the World Wide Web and subsequent work on computer network protocols. Currently he works on encapsulating <a href="https://azure.microsoft.com/en-us/blog/bringing-ai-to-the-edge/">Machine Learning models into containers</a>. Our manager, <a href="https://www.linkedin.com/in/pabloc/">Pablo Castro</a> started not only Azure Search, but also <a href="https://hanselminutes.com/205/open-data-protocol-odata-with-pablo-castro">OData</a> protocol and <a href="https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities">LINQ to Entities</a>. Our Project Manager <a href="https://www.linkedin.com/in/lance-olson-513bb816/">Lance Olson</a> was one of the founders of the .NET! You can check out what people say about our team on <a href="https://www.teamblind.com/search/azure%20search">blind</a>! Search for "Azure Search" ;) There is also a blog post written by Pablo a few years ago: <a href="https://medium.com/@pabloc/a-startup-at-microsoft-43dd2a78b9f5">Startup at Microsoft</a>. A lot has changed since then. We went through a few rounds of "funding", and our team grew. However, we still believe in core values expressed there. For example: every engineer from the team still talks to customers on daily basis either through social media or directly over email or Skype.</p>
<p>BTW: We are hiring!</p>

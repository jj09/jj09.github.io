---
layout: post
title: QCon conferences - real experts experience exchange
date: 2018-07-04 11:02:30.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- events
- programming
tags:
- Azure
- AzureSearch
- brazil
- china
- QCon
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
  dsq_thread_id: '6773179386'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/qcon-conferences-real-experts-experience-exchange/"
---
<p><img class="aligncenter size-full wp-image-19578" src="{{ site.baseurl }}/assets/2018/07/qcon-beijing-speakers.jpg" alt="QCon Beijing - speakers" width="900" height="246" /></p>
<p>Earlier this year I attended <a href="https://2018.qconbeijing.com">QCon Beijing</a> and <a href="https://qconsp.com/">QCon Sao Paulo</a> conferences. I really like QCon, because there is no marketing, just real experts exchange of experience. After my first QCon (<a href="https://jj09.net/qcon-shanghai/">Shanghai in 2016</a>) I was very excited to come back this year!</p>
<h3>QCon Beijing</h3>
<h4>Cognitive Search</h4>
<p>I delivered talk about <a href="https://2018.qconbeijing.com/presentation/451">Building web apps with Cloud and AI</a>. I showed how to build intelligent web apps with Azure Search and Cognitive Services (Azure Machine Learning APIs). We call this approach Cognitive Search. In my demo I showcased how you can determine which crypto currencies to buy using sentiment analysis on tweets. I streamed tweets to Event Hub, which triggers Azure Function that calls Text Analytics API to calculate sentiment of tweet. I store tweets and its sentiments in SQL Database. I also created Azure Search index to be able to effectively search through tweets. This index is being syncronized with SQL DB through <a href="https://docs.microsoft.com/en-us/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers#sql-integrated-change-tracking-policy">integrated change tracking</a>, and <a href="https://docs.microsoft.com/en-us/azure/search/search-indexer-overview">Azure Search indexer</a> that runs on schedule.</p>
<p><img class="aligncenter size-full wp-image-19606" src="{{ site.baseurl }}/assets/2018/07/cognitive_search_architecture.png" alt="Cognitive Search architecture" width="600" height="370" /></p>
<p>I built UI using <a href="https://github.com/jj09/AzSearch.js">AzSearch.js</a> (UI generation tool for Azure Search indexes), ASP.NET Core and TypeScript (BTW: there is a lot of cool stuff in <a href="https://www.youtube.com/watch?v=hDACN-BGvI8">TypeScript</a> these days!).</p>
<p><img class="aligncenter size-full wp-image-19636" src="{{ site.baseurl }}/assets/2018/07/CryptoSearchUI.png" alt="Crypto Search UI" width="1280" height="682" /></p>
<p>In addition to search interface I also created aggregation chart comparing sentiments between different cryptos:</p>
<p><img class="aligncenter size-full wp-image-19634" src="{{ site.baseurl }}/assets/2018/07/CryptoCharts.png" alt="crypto charts" width="1280" height="590" /></p>
<p>Source code is on github: <a href="http://github.com/jj09/crypto-search">crypto-search</a>.</p>
<p>Video from my talk:</p>
<div class="aligncenter" style="margin: 20px;"><iframe src="https://www.youtube.com/embed/Gzwq6JC6qwY?ecver=1" width="640" height="360" frameborder="0" allowfullscreen="allowfullscreen"></iframe></div>
<p>My talk was very well received. Attendees were assessing talks with green (great talk), yellow (ok talk) and red (bad talk) cards. I got <b>117 green</b>, <b>9 yellows</b> and <b>0 reds</b>.</p>
<h4>Conference</h4>
<p>I had a great opportunity to meet a lot of engineers and architects from leading tech companies from around the World.</p>
<p><a href="https://twitter.com/madstorgersen">Mads Torgersen</a> (the architect of C# language) shared future plans for C#. It was surprising for me how few people attended his talk. <a href="https://twitter.com/Miaomipao">Sisie Xia</a> and Chris Coleman from LinkedIn delivered a great talk about facing challenge of growth, and how they tackle it using their in-house tool <a href="https://engineering.linkedin.com/blog/2017/02/redliner--how-linkedin-determines-the-capacity-limits-of-its-ser">Redliner</a>. <a href="https://github.com/juliusv">Julius Volz</a> shared insights about <a href="https://prometheus.io/">Prometheus</a> monitoring system.</p>
<p>Majority of talks were in Chinese. I went to <a href="https://2018.qconbeijing.com/presentation/360">Peng Xing</a>'s talk about how they develop Progressive Web Apps at Baidu. I was able to gather 60% of content, but got the essence by talking to him directly. I spent most of my time talking to people in the hallways. It was very eye opening to meet engineers from Chinese cloud giants. China cloud market is dominated by <a href="https://www.alibabacloud.com">Alibaba Cloud (AliCloud)</a>, <a href="https://www.baidu.com">Baidu</a> and <a href="https://intl.cloud.tencent.com">Tencent</a>. Azure and AWS have small market share. Google does not exists in China at all. Alibaba (largest online retailer in China) has even <a href="http://www.scmp.com/tech/enterprises/article/2114965/alibaba-says-it-track-overtake-amazon-worlds-top-cloud-computing">ambitions to overtake AWS</a> in near future. It is worth to notice that Alibaba is Chinese equivalent of Amazon. At the same time people consider Baidu being Chinese Google, and Tencent (who owns WeChat) to be like Facebook. I had an opportunity to chat with <a href="https://2018.qconbeijing.com/presentation/368">Lu</a> from Alibaba Cloud and <a href="https://2018.qconbeijing.com/presentation/440">Wang Yao</a> (Head of IaaS at Baidu). After talking to them, and other engineers I would describe both companies' stack in 3 Words: MacBook, Java and Go. This might be ignorant generalization, but almost every other engineer from big 3 (AliCloud, Baidu, Tencent) that I talked to was either writing code in Java or golang (using Mac of course). I also learned about Alibaba's Search as a Service: OpenSearch. Something to keep eye on when they will be expanding to USA and Europe market.</p>
<p>The most popular track was of course Blockchain. Room was overflowed for the entire day:</p>
<p><img class="aligncenter size-full wp-image-19610" src="{{ site.baseurl }}/assets/2018/07/qcon_beijing_blockchain.png" alt="QCon Beijing - blockchain track" width="550" height="451" /></p>
<h4>China Tech</h4>
<p>Every time when I visit China I am impressed by their progress. Highways superior to US interstates, fast trains between all major cities, and now - mobile payments adoption everywhere. Today, in China, most people use WeChat or AliPay. Sometimes cashier can get mad at you if you want to pay cash or credit card, because you cause inconvenience. Scanning QR code is 10x faster! You can even tip a waiter with your mobile phone!</p>
<p><img class="aligncenter size-full wp-image-19597" src="{{ site.baseurl }}/assets/2018/07/tippinginchina.gif" alt="Tipping in China" width="480" height="480" /></p>
<p>Last year in Seattle we had <a href="https://www.geekwire.com/2017/hello-yellow-bikes-testing-ofo-third-bike-sharing-service-hit-seattles-streets/">three bike-sharing companies</a>, and everybody here thinks that we are at the edge of innovation. By the end of 2017 Beijing had <a href="http://money.cnn.com/2017/12/29/investing/china-bike-sharing-boom-bust">60 bike-sharing companies</a>. Many of them started in 2016. During my visit I learned that <a href="https://gineersnow.com/leadership/chinese-government-dominated-scientists-engineers">China have engineers dominated government</a>. Maybe this explains their progress?</p>
<p>If you are going to China, it is useful to have these 3 apps:<br />
1. <a href="https://wechat.com">WeChat</a> - Chinese facebook, for communication with other Chinese people, and exchanging contacts<br />
2. <a href="https://www.didiglobal.com/">DiDi</a> - Chinese Uber<br />
3. <a href="https://intl.alipay.com/">AliPay</a> - for mobile payments (currently WeChat payments requires Chinese ID and account in Chinese Bank)</p>
<p>It was also great to meet China division of Cognitive Services team!</p>
<p><img class="aligncenter size-full wp-image-19622" src="{{ site.baseurl }}/assets/2018/07/CognitiveServices-China.png" alt="Cognitive Services - China team" width="800" height="466" /></p>
<p>Trip to China inspired me to read a book comparing Chinese and Western culture in the World of innovation and progress:</p>
<p><a href="https://amzn.to/2tOQiGi"><img class="aligncenter size-full wp-image-19628" src="{{ site.baseurl }}/assets/2018/07/FromGreatWallToWallStreet.jpg" alt="From the Great Wall to Wall Street" width="343" height="499" /></a></p>
<p>There is a lot of things that these two Worlds can learn from each other.</p>
<h3>QCon Sao Paulo</h3>
<h4>Cognitive Search</h4>
<p>Two days before my talk in Brazil, we officially announced <a href="https://jj09.net/cognitive-search-azure-search-with-ai/">Cognitive Search</a> built in into Azure Search. You do not have to create Cognitive Service anymore. You do not have to write code that orchestrate processing data, and calling API. We do it for you. All what you have to do is to check the checkbox. More details <a href="https://jj09.net/cognitive-search-azure-search-with-ai/">here</a>.</p>
<p><img class="aligncenter size-full wp-image-19560" src="{{ site.baseurl }}/assets/2018/07/grok-overview.png" alt="Cognitive Search" width="721" height="355" /></p>
<p>I extended my demo of crypto analysis based on tweets by adding sentiment analysis on news articles. A while ago we put news into Azure Search index. We filtered out news related to cryptos, and put it on Azure Blob storage. We also improved our <a href="https://channel9.msdn.com/Shows/AI-Show/Using-Cognitive-Search-to-Understand-the-JFK-Documents">JFK files demo</a>, and now you can deploy it by yourself by following instructions in <a href="https://github.com/Microsoft/AzureSearch_JFK_Files">this github repo</a>.</p>
<p>Video from my talk:</p>
<p><iframe width="640" height="360" src="https://www.youtube.com/embed/9hYxHHIJ_Kk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></p>
<p>Usually during my talk I ask if somebody ever deployed ElasticSearch and how long did it take. In China one guy said it was ~2 weeks. In Brazil there was one guy who said: 6 months(!) :) That's why you don't want this to be your problem. Azure Search takes care of deployment, availability and upgrades for you.</p>
<p>My talk was pretty well received in Brazil as well. I got <b>148 green</b>, <b>15 yellow</b> and <b>0 red</b> cards.</p>
<h4>Conference</h4>
<p>QCon Sao Paulo had very diverse mix of experts from all around the World. Starting with <a href="https://twitter.com/aaronontheweb">Aaron Stannard</a> (co-founder of <a href="https://getakka.net/">AKKA.NET</a>), <a href="https://twitter.com/nikomatsakis">Nicholas Matsakis</a> (from <a href="https://www.rust-lang.org">Rust</a> core team), and <a href="https://twitter.com/kumpera">Rodrigo Kumpera</a> (architect and top contributor of <a href="https://www.mono-project.com/">mono</a> project), through <a href="https://twitter.com/texasmichelle">Michelle Casbon</a> (now Engineer in Google Cloud Platform focused on machine learning and big data tools), <a href="https://twitter.com/BenLesh">Ben Lesh</a> (RxJS Lead at Google), and <a href="https://martinspier.io/">Martin Spier</a> (performance engineer at Netflix) to <a href="https://twitter.com/soupsranjan">Soups Ranjan</a> (Director of Data Science at Coinbase*), <a href="https://twitter.com/amcasari">Amanda Casari</a> (Data Scientist at SAP Concur), and <a href="https://github.com/piperniehaus">Piper Niehaus</a> (Elm lang passionate).</p>
<p>The most interesting thing I learned at QCon Sao Paulo was how different companies struggle with monitoring, telemetry and system malfunction detection. They all have very sophisticated automation, but it is still not enough in today's World complexity. As systems we build have more, and more complex architecture, we need to build even better monitoring software to maintain them.</p>
<p>In Azure Search we are using <a href="http://www.odata.org/">OData</a> standard. However, recently <a href="https://graphql.org/">GraphQL</a> is gaining popularity. <a href="https://twitter.com/dmcghan">Dan McGhan</a> shared this article about comparing GraphQL and OData: <a href="https://www.progress.com/blogs/rest-api-industry-debate-odata-vs-graphql-vs-ords">REST API Industry Debate: OData vs GraphQL vs ORDS</a>. Interesting read!</p>
<h4>Brazil</h4>
<p>May is almost winter in Brazil, but it's also the best time to visit. Not too hot, not too cold. Perfect weather for enjoying your time!</p>
<p>I like that every bar and restaurant in Brazil have TV on soccer channel :) As a long standing fan of Brazil national football team (since <a href="https://www.youtube.com/watch?v=y-P8owvfsOs">Ronaldo Luiz Nazario de Lima</a> times) I enjoyed it a lot!</p>
<p>Sao Paulo, the largest city in Brazil (21 million people) and financial center of the country, is also the largest tech-hub in south America. Most of tech-companies are there (Microsoft, Google, Amazon).</p>
<p>If you ever go to Brazil, remember to visit <a href="https://en.wikipedia.org/wiki/Sugarloaf_Mountain">Sugarloaf</a> to watch the sunset and after the sunset view :)</p>
<p><img class="aligncenter size-full wp-image-19616" src="{{ site.baseurl }}/assets/2018/07/sugarlof.png" alt="View from Sugarloaf after night" width="800" height="374" /></p>
<h3>Summary</h3>
<p>Speaking at QCons and connecting with engineers from different backgrounds is very valuable experience. Being able to learn about other cultures is a plus as well. Sharing with other work that you do everyday can also give you different perspective, and notice things that you would never think about.</p>
<p>If you want to learn more about Azure Search check out our <a href="https://docs.microsoft.com/en-us/azure/search/search-get-started-portal">getting started docs</a>. To create intelligent search pipelines check out my <a href="https://jj09.net/cognitive-search-azure-search-with-ai">Cognitive Search</a> blog post. For more details we have <a href="https://docs.microsoft.com/en-us/azure/search/cognitive-search-quickstart-blob">quickstart</a> and more comprehensive <a href="https://docs.microsoft.com/en-us/azure/search/cognitive-search-tutorial-blob">API overview</a>.</p>
<p>Questions? Find me on <a href="https://twitter.com/realJacobJed">twitter</a>!</p>
<p><em>*Soups did not tell me what is the next coin coming to CoinBase :(</em></p>

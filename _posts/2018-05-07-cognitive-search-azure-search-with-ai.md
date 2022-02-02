---
layout: post
title: Cognitive Search - Azure Search with AI
date: 2018-05-07 14:58:15.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- Azure
- AzureSearch
- CognitiveServices
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
  dsq_thread_id: '6657659213'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/cognitive-search-azure-search-with-ai/"
---
<p><img class="aligncenter size-full wp-image-19560" src="{{ site.baseurl }}/assets/2018/05/grok-overview.png" alt="Cognitive Search" width="721" height="355" /></p>
<p>Today, at <a href="https://developer.microsoft.com/en-us/events/build">Microsoft //build conference</a> we announced Cognitive Search. You may wonder what is Cognitive Search. To put it as simple as possible: it’s Azure Search powered by <a href="https://azure.microsoft.com/en-us/services/cognitive-services/">Cognitive Services</a> (Azure Machine Learning APIs). You remember when you wanted to run some intelligence over your data with <a href="https://azure.microsoft.com/en-us/services/cognitive-services/">Cognitive Services</a>? You had to handle creating, e.g., <a href="https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/">Text Analytics API</a>, then writing code that would take your data from database, issue request to API (remember to use proper key!), serialize, deserialize data and put result in your database?</p>
<p>Now, with Cognitive Search, you can achieve that by checking one checkbox. You just need to pick a field on which you want to run analytics, and which cognitive services or skills (1 cognitive service usually contain multiple skills) to run. As for now we support 6 skills:</p>
<ol>
<li>Key phrases</li>
<li>People</li>
<li>Places</li>
<li>Organizations</li>
<li>Language</li>
<li>OCR (Optical Character Recognition)</li>
</ol>
<p>We output results directly to your search index.</p>
<h3>Creating Intelligent Search Index</h3>
<p>To take advantage of Cognitive Search you need to create Azure Search service in South-Central US or in West Europe. More regions coming soon!</p>
<p>To create search index powered by cognitive services you need to use ‘import data’ flow. Go to your Azure Search Service and click on ‘Import data’ command:</p>
<p><img class="aligncenter size-full wp-image-19547" src="{{ site.baseurl }}/assets/2018/05/grok-step1-e1525702355364.png" alt="Cognitive Search - step 1" width="640" height="295" /></p>
<p>Then pick your data source (MSSQL, CosmosDB, blob storage etc.). I will choose sample data source that contains real estate data:</p>
<p><img class="aligncenter size-full wp-image-19548" src="{{ site.baseurl }}/assets/2018/05/grok-step2-e1525702491696.png" alt="Cognitive Search - import data" width="640" height="293" /></p>
<p>Now, you need to pick a field on which you want to run analytics. I will choose description. You also need to choose which cognitive services (skills) you want to run, and provide output field names (fields to which we will output cognitive services analysis result):</p>
<p><img class="aligncenter wp-image-19549 size-full" src="{{ site.baseurl }}/assets/2018/05/grok-step3-e1525702970533.png" alt="Cognitive Search - skillset definition" width="640" height="355" /></p>
<p>In the next step you need to configure your index. Usually you want to make fields retrievable, searchable, and filterable. You may also consider making them facetable if you want to aggregate results. This is my sample configuration:</p>
<p><img class="aligncenter size-full wp-image-19550" src="{{ site.baseurl }}/assets/2018/05/grok-step4-e1525703032502.png" alt="Cognitive search - define index" width="641" height="292" /></p>
<p>In the last step you just need to configure indexer – a tool that synchronizes your data source with your search index. In my case I will choose to do synchronization only once, as my sample data source will never change.</p>
<p><img class="aligncenter size-full wp-image-19551" src="{{ site.baseurl }}/assets/2018/05/grok-step5-e1525703179232.png" alt="Cognitive Search - create indexer" width="640" height="290" /></p>
<p>After indexer finish you can browse your data, and cognitive services results in search explorer.</p>
<p><img class="aligncenter size-full wp-image-19552" src="{{ site.baseurl }}/assets/2018/05/grok-browse-e1525703442307.png" alt="Cognitive Search - browse" width="640" height="291" /></p>
<p>You can also generate more usable search UI for your data with AzSearch.js.</p>
<h3>Generating UI to search data with AzSearch.js</h3>
<p>If you don’t like browsing your data with search explorer in Azure Portal that returns raw JSON, you can use <a href="https://github.com/jj09/AzSearch.js">AzSearch.js</a> to quickly generate UI over your data.</p>
<p>The easiest way to get started is to use <a href="http://azsearchstore.azurewebsites.net/azsearchgenerator/index.html">AzSearch.js generator</a>. Before you start, enable CORS on your index:</p>
<p><img class="aligncenter size-full wp-image-19554" src="{{ site.baseurl }}/assets/2018/05/grok-cors-e1525703959825.png" alt="Cognitive search - CORS" width="641" height="292" /></p>
<p>Once you get your <a href="https://docs.microsoft.com/en-us/azure/search/search-query-rest-api#identify-your-azure-search-services-query-api-key">query key</a> and <a href="https://docs.microsoft.com/en-us/rest/api/searchservice/get-index">index definition JSON</a> paste it into <a href="http://azsearchstore.azurewebsites.net/azsearchgenerator/index.html">generator</a> together with your search service name, and click 'Generate'. An html page with simple search interface will be created.</p>
<p><img class="aligncenter size-full wp-image-19555" src="{{ site.baseurl }}/assets/2018/05/grok-azsearchjs-e1525707951525.png" alt="Cognitive Search - AzSearch.js" width="639" height="294" /></p>
<p>This site is super easy to customize. Providing html template for results change JSON into nicely formatted search results:</p>
<p><img class="aligncenter size-full wp-image-19557" src="{{ site.baseurl }}/assets/2018/05/grok-azsearch-pretty-e1525705132550.png" alt="Cognitive search - AzSearch.js pretty" width="640" height="292" /></p>
<p>All what I did was to create HTML template:</p>
{% highlight javascript %}
{% raw %}
const resultTemplate =
    `<div class="col-xs-12 col-sm-5 col-md-3 result_img">
        <img class="img-responsive result_img" src="{{ site.baseurl }}/assets/2018/05/{{thumbnail}}" alt="image not found" />
    </div>
    <div class="col-xs-12 col-sm-7 col-md-9">
        <h4>{{displayText}}</h4>
        <div class="resultDescription">
            {{summary}}
        </div>
        <div>
            sqft: <b>{{sqft}}</b>
        </div>
        <div>
            beds: <b>{{beds}}</b>
        </div>
        <div>
            baths: <b>{{baths}}</b>
        </div>
        <div>
            key phrases: <b>{{keyPhrases}}</b>
        </div>
    </div>`;
    {% endraw %}
{% endhighlight %}
<p>And add it to already present <code>addResults</code> function call:</p>
{% highlight javascript %}automagic.addResults("results", { count: true }, resultTemplate);
{% endhighlight %}
<p>I also created <code>resultsProcessor</code> to do some custom transformations. I.e., join few fields into one, truncate description to 200 characters, and convert key phrases from array into string separated by commas:</p>
{% highlight javascript %}
var resultsProcessor = function(results) {
    return results.map(function(result){
        result.displayText = result.number + " " + result.street+ " " +result.city+ ", " +result.region+ " " +result.countryCode;
        var summary = result.description;
        result.summary = summary.length &lt; 200 ? summary : summary.substring(0, 200) + "...";
        result.keyPhrases = result.keyphrases.join(", ");
        return result;
    });
};
automagic.store.setResultsProcessor(resultsProcessor);
{% endhighlight %}
<p>You can do similar customization with suggestions. You can also add highlights to your results and much more. Everything is described in <a href="https://github.com/jj09/AzSearch.js/blob/master/README.md">AzSearch.js README</a>. We also have <a href="https://github.com/jj09/AzSearch.jsTypeScriptStarter">starter app written with TypeScript and React</a> based on sample real estate data, which takes advantage of more advanced features of <a href="https://github.com/jj09/AzSearch.js">AzSearch.js</a>. If you have any questions or suggestions regarding AzSearch.js let me know on <a href="https://twitter.com/JakubJedryszek">Twitter</a>!</p>
<h3>Summary</h3>
<p>Cognitive Search takes analyzing data with Azure Search to the next level. It takes away the burden of writing your own infrastructure for running AI-based analysis. For more advanced analysis, including OCR on your images, check out <a href="https://docs.microsoft.com/en-us/azure/search/cognitive-search-quickstart-blob">our docs</a>. I am super excited to see it in action, and for the next improvements that we are working on. Let us know what do you think!</p>
<p><em>*This blog post was written in Boeing 787 during my flight from Toronto to São Paulo, when I was on my way to <a href="https://qconsp.com/sp2018/presentation/building-web-apps-cloud-and-ai">QCon conference</a>.</em></p>

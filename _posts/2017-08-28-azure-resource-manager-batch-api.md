---
layout: post
title: Azure Resource Manager Batch API
date: 2017-08-28 08:41:41.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- Azure
- AzureApp
- C#
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
  dsq_thread_id: '6102243162'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/azure-resource-manager-batch-api/"
---
<p>The latest Azure Mobile App update has statuses on the resources list:</p>
<p><img class="aligncenter size-full wp-image-18563" src="{{ site.baseurl }}/assets/2017/08/AzureAppStatuses-e1502211629995.jpg" alt="Azure App - Statuses on resources list" width="300" height="534" /></p>
<p>You probably want to ask why we didn't have them before. Great question! Currently <a href="https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview">Azure Resource Manager</a> (public API we are using to get your Azure resources) requires to make separate calls to get single resource status. It means: if you have 100-200 resources, you would have to make 100-200 extra calls. There are some people who has almost 2000 in one subscription! Taking performance and data usage into consideration, this is not ideal.</p>
<p>Both iOS and Android platforms allows to address this problem to some extent by querying for status only resources that are currently visible. However this is still extra 5-10 calls. It is even worse when you start scrolling, and very bad if you scroll on your list containing 2000 resources.</p>
<h3>Batch API</h3>
<p>Sometime ago <a href="https://docs.microsoft.com/en-us/rest/api/batchservice/">ARM</a> added <a href="https://msdn.microsoft.com/en-us/skype/ucwa/batchingrequests">Batch API</a> - you can send POST request with up to 20 URIs in the body. Response will contain up to 20 packaged responses that you have to extract. Using batch API, you can decrease number of requests by up to 20x. This matters especially when user has a lot of resources and keep scrolling on the list.</p>
<p>When implementing batch requests, you need to figure out the optimal interval for sending requests. We started with 200ms, but then we changed it to 50ms. Additionally, every time new request is coming we delay sending batch request by additional 50ms. This may cause indefinite delay. In order to solve this: we always submit request if queue has 20 or more pending requests. 20*50ms = 1000ms = 1s = long time! We tweaked it again, and changed interval to 20ms. With current implementation, we wait anytime between 20ms and 400ms to send batch request.</p>
<h3>Implementing Batch API</h3>
<p>You probably gonna say: "it all sounds great, but how do I implement it"? For you convenience I created small console application that demonstrate ARM Batch API in action, and I put it on <a href="https://github.com/jj09/ArmBatchApi">github</a>.</p>
<p>Xamarin.iOS and Xamarin.Android does not have <code>System.Threading.Timer</code>. We created our own implementation <code>OneShotTimer</code> (thanks William Moy!).</p>
<p>Entire magic happens in <em>ArmService</em>. It has one public method <code>GetResource</code> that instead of directly sending GET request is adding request to <em>ConcurrentQueue</em>. <code>OneShotTimer</code> and <code>BatchRequestDipatcher</code> methods are responsible for sending the actual HTTP request.</p>
<p>In order to run console app, you need to provide ARM token, and (optionally) resource ids you want to request. In demo app I provided fake resource ids, which will be fine to issue requests, but you will not get resource back.</p>
<p>To get ARM token, go to Azure Portal, open F12 tools and inspect some ARM request. From request headers, copy <em>Authorization</em> header (string starting with <tt>Bearer rAnDoMcHaRacTErS...</tt>):</p>
<p><img class="aligncenter size-full wp-image-18743" src="{{ site.baseurl }}/assets/2017/08/AzurePortalToken-e1502985354279.png" alt="Azure Portal - ARM token" width="800" height="528" /></p>
<p>You can also get resources ids from F12 tab. The best way is to go to All Resources blade, and find some batch request:</p>
<p><img class="aligncenter size-full wp-image-18763" src="{{ site.baseurl }}/assets/2017/08/AzurePortalResourceIds-e1502985461123.png" alt="Azure Portal - resources ids" width="799" height="529" /></p>
<p>Once you paste resource ids and ArmToken in Program.cs you can run the app, and you should see the following output:</p>
<p><img class="aligncenter size-full wp-image-18783" src="{{ site.baseurl }}/assets/2017/08/Batch5000ms-e1502987360917.png" alt="Batch requests with 5s randomness" width="800" height="908" /></p>
<p>Requests are send in random time, anytime from 0 to 5s after program runs. This is done using <em>Task.Delay</em>:</p>
{% highlight csharp %}
var tasks = _resourceIds.Select(async resourceId =>
{
  await Task.Delay(new Random().Next() % 5000);   // simulate calling GetResource from different parts of UI
  var response = await _armService.GetResource(resourceId);
  resources.Add(response);
});
{% endhighlight %}
<p>When you change randomness from 5s to 0.5s you can observe that there will be less batch requests (AKA more requests sent in single batch):</p>
<p><img class="aligncenter size-full wp-image-18803" src="{{ site.baseurl }}/assets/2017/08/Batch500ms-e1502987628893.png" alt="Batch requests with 0.5s randomness" width="800" height="910" /></p>
<h3>Summary</h3>
<p>Using Batch API for getting resource statuses visibly improves performance in the mobile app. It is noticeable especially when using network data.</p>
<p>Azure Resource Manager has plans to add ARM API that will allow to do 1 request to get multiple resources with statuses. This should improve performance even more in the future.</p>
<p>If you are facing similar problem with your app, consider implementing Batch API on your server!</p>

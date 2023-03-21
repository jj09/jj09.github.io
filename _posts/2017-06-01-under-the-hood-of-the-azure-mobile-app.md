---
layout: post
title: Under the hood of the Azure Mobile App
date: 2017-06-01 20:18:00.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- ".NET"
- Azure
- Azure Portal
- C#
- mobile
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
  dsq_thread_id: '5872103196'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/under-the-hood-of-the-azure-mobile-app/"
---
<p style="text-align: center;"><img class="size-full wp-image-17711" style="float: left; margin: 10px;" src="{{ site.baseurl }}/assets/2017/06/AzureApp-Resources.png" alt="" width="200" height="356" /></p>
<p><img class="size-full wp-image-17701" style="float: left; margin: 10px;" src="{{ site.baseurl }}/assets/2017/06/AzureApp-Resource.png" alt="" width="200" height="356" /></p>
<p><img class="size-full wp-image-17691" style="float: left; margin: 10px;" src="{{ site.baseurl }}/assets/2017/06/AzureApp-Notifications.png" alt="" width="200" height="356" /></p>
<p><img class="size-full wp-image-17681" style="margin: 10px;" src="{{ site.baseurl }}/assets/2017/06/AzureApp-Console.png" alt="" width="200" height="356" /></p>
<p>For last 6 months I've been working on <a href="https://thenextweb.com/dd/2017/05/10/microsoft-announces-new-azure-mobile-applications-android-ios/">the Azure Mobile App</a> for iOS and Android. We officially announced it at Microsoft's <a href="https://build.microsoft.com/">//build</a> conference keynote last month.</p>
<p><iframe src="https://www.youtube.com/embed/YKK_XHMFE3U?start=594&amp;end=639" width="854" height="480" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>
<p>Now, you can monitor your Azure Resources from your phone! You can also take quick management actions, like start/stop/restart. Actually, you can do whatever you want using Cloud Shell that enables you to execute any command available through Azure CLI and PowerShell.</p>
<p>To learn more about the app functionalities, check out <a href="https://twitter.com/flanakin">Michael Flanakin</a>'s blog post: <a href="https://azure.microsoft.com/en-us/blog/azure-app-preview/">Introducing the Azure app public preview</a>.</p>
<h3>Xamarin</h3>
<p>The app is built with Xamarin Native in C#. To learn more about Xamarin, checkout my blog post <a href="https://jj09.net/getting-started-with-xamarin-in-2016/">Getting started with Xamarin in 2016</a>.</p>
<p>The great thing about Xamarin Native apps is the fact that you can do everything what is possible when building native iOS apps with swift and native Android apps with Java. You can take any code sample in swift or Java, translate it to C# and use in your Xamarin app. Additionally, you can share code across platforms. We have around 60-70% code share. Most of our code is shared using PCL (Portable Class Library). Some components are in Shared Project.</p>
<p><img class="aligncenter size-full wp-image-18131" src="{{ site.baseurl }}/assets/2017/06/AzureMobileSolution.png" alt="Azure Mobile Solution" width="532" height="422" /></p>
<h3>Continuous Integration and Continuous Delivery with VSTS and Hockey App</h3>
<p><a href="https://www.visualstudio.com/team-services/">VSTS</a> provide awesome tools for customizing build params, running tests, and deploying with HockeyApp (now [replaced by Visual Studio App Center](https://devblogs.microsoft.com/appcenter/hockeyapp-is-being-retired/))</a>. What's more, when you are publishing your alpha/beta builds with HockeyApp you get auto-update notifications for free.</p>
<p>We have 3 environments:</p>
<ul>
<li>alpha - deployed on every commit if tests are passing (used by team members)</li>
<li>beta - deployed after merge from alpha branch if all tests are passing (available for all Microsoft employees - it allows us to test the next release candidate)</li>
<li>App Store / Google Play - deployed manually (Apple does not provide mechanism to auto-deploy and we are working on automating Google Play deploy from VSTS)</li>
</ul>
<h4>Build definitions</h4>
<p>I blogged about <a href="https://jj09.net/continuous-integration-and-continuous-delivery-for-xamarin-ios-with-vsts/">setting up VSTS for Xamarin.iOS</a> earlier this year. Configuring Android build is much easier. Our VSTS build pipelines for iOS and Android look like below.</p>
<p style="text-align: center;"><img class="aligncenter size-full wp-image-17751" style="float: left; margin: 10px;" src="{{ site.baseurl }}/assets/2017/06/VSTS-ios.png" alt="VSTS Xamarin.iOS build definition" width="400" height="832" /></p>
<p><img class="aligncenter size-full wp-image-17781" style="margin: 10px;" src="{{ site.baseurl }}/assets/2017/06/VSTS-droid-1.png" alt="VSTS - Xamarin.Droid build definition" width="400" height="1003" /></p>
<p>The general scenario is:</p>
<ul>
<li>build in <em>Debug</em> mode (in order to initialize TestCloud, which I described in <a href="https://jj09.net/continuous-integration-and-continuous-delivery-for-xamarin-ios-with-vsts/">this blog post</a>)</li>
<li>run tests</li>
<li>build in <em>Release</em> mode (without TestCloud init code)</li>
<li>deploy to HockeyApp</li>
</ul>
<p>We are thinking about running tests in <em>Release</em> mode (it requires passing <em>TEST_CLOUD</em> build param to build command explicitly). This will give us the same app that later on will be deployed to HockeyApp. A few times we had situations when app was working fine in <em>Debug</em> mode and all UI tests were passing, but it was crashing on startup in Release mode. In this case, if somebody updated app on their device, they had to uninstall it, and install manually again after we fixed bug causing crash. Very inconvenient.</p>
<h4>Storing secrets</h4>
<p>VSTS provides mechanism to keep your secrets (passwords and tokens) outside of your source code. You can store them in <em>Variables</em> tab in your build definition. Notice small lock next to secret value. Once you click it, it will hide the secret forever. There is no way to read it back from VSTS. I've done this a few times, and had to regenerate keys and tokens. You can store your secrets in <a href="https://azure.microsoft.com/en-us/services/key-vault/">Azure KeyVault</a>, where they are always readable.</p>
<p><img class="aligncenter size-full wp-image-17851" src="{{ site.baseurl }}/assets/2017/06/VSTS-variables.png" alt="VSTS - variables" width="1868" height="800" /></p>
<p>When you are running UI tests, usually you need to authenticate (AKA you need password to login with your test account). There is no way to pass password as parameter to Test Cloud, but there is a workaround: we have file <em>Password.txt</em> in UI test project (without password of course), and before running UI tests, we run shell script that takes password (from VSTS <em>Variables</em>) as parameter and writes it to the Password.txt file. You can pass variables stored in VSTS as arguments to VSTS tasks.</p>
<p>This is shell script:</p>

{% highlight csharp %}
#!/bin/bash
echo $1 > $2/Tests/AzureMobile.UITests/password.txt
{% endhighlight %}

<p>And this is VSTS task:</p>
<p><img class="aligncenter size-large wp-image-17961" src="{{ site.baseurl }}/assets/2017/06/GetPasswordForTestCloud-785x456.png" alt="GetPasswordForTestCloud" width="785" height="456" /></p>
<p>VSTS is awesome! It allows you to do almost anything with VSTS tasks or custom scripts. You can modify version number in Info.plist file before building solution, <a href="https://jj09.net/hockeyapp-vsts-generate-release-notes-from-last-git-commit-message/">add release notes from git commit messages</a> and much, much more.</p>
<h3>UI tests with Xamarin Test Cloud</h3>
<p>TestCloud is awesome. It allows you not only automate UI testing. It also enables you to test your app on hundreds of devices without need of buying any of them.</p>
<p>UI tests are usually the longest running task in our build pipeline. In order to minimize wait times between builds, we run UI tests only on one, most reliable device. We have separate build definitions to run UI tests nightly on 20 iOS and 40 Android devices. It takes longer, but it helps us to identify issues related to particular device model. Most of the time we don't have changes that are breaking single device.</p>
<p>We are also thinking about creating 1-2 smoke tests that will be run on every commit, and run entire suite nightly or on separate build (to don't block other runs).</p>
<h4>Don't assert! Use WaitFor!</h4>
<p>UI testing 101: when you are writing UI tests, remember to wait for UI to update before asserting some condition. E.g., let's say you have button and label. After button click, you expect label to update its text to 'Button clicked'. Below test will be very flakey:</p>

{% highlight csharp %}
app.Tap("myButton");
Assert.AreEqual("Button clicked", app.Query("myLabel").Label);
{% endhighlight %}

<p>Label may not get updated before assertion gets executed. Instead you should use WaitFor:</p>

{% highlight csharp %}
app.Tap("myButton");
app.WaitFor(app.Query("myLabel").Label.Equals("Button clicked", StringComparison.InvariantCulture));
{% endhighlight %}

<h4>Page Object Pattern</h4>
<p>Another very good practice for writing UI tests is to use <a href="https://github.com/xamarin/customer-success-samples/blob/a51ad4ef949059f7260c3d3af45b701f6dd55503/samples/Snippets/PageObjectPatternExample/README.md">Page Object Pattern</a>. This allows you to isolate implementation details from tests scenarios.</p>
<p>Here is one of our tests:</p>

{% highlight csharp %}
[Test]
public void Favorites_AddToFavorites_ResourceVisibleOnFavoritesPage()
{
    // Arrange
    var resourceToFavorite = TestResources.Azurembwinvm;
    TapTabBarItem(Strings.Resources);

    // Act
    _resourcesPage.TapResourceByName(resourceToFavorite);
    _resourceDetailsPage.VerifyPresent();
    _resourceDetailsPage.ExecuteCommand(Strings.Favorite, Strings.Unfavorite);
    _resourceDetailsPage.GoBack();

    // Assert
    TapTabBarItem(Strings.Favorites);
    _favoritesPage.VerifyPresent();
    _favoritesPage.VerifyNavBarTitle(1);
    _favoritesPage.WaitForResourceByName(resourceToFavorite);
}
{% endhighlight %}

<p>Here, are some methods implemented in Page class:</p>

{% highlight csharp %}
public FavoritesPage WaitForResourceByName(string resourceName)
{
    _app.Screenshot($"Waiting for resource {resourceName}...");

    _app.WaitForElement(resourceName);

    return this;
}

public FavoritesPage TapResourceByName(string resourceName)
{
    _app.Screenshot($"Tapping resource '{resourceName}'...");

    _app.WaitForAndTapOnElement(resourceName);

    return this;
}

public FavoritesPage WaitForNoResourceByName(string resourceName)
{
    _app.Screenshot($"Checking if resource '{resourceName}' is not present...");

    _app.WaitForNoElement(resourceName);

    return this;
}
{% endhighlight %}

<h4>Screenshots during UI tests</h4>
<p>As you probably noticed in above code snippet, we are taking screenshots at almost every step. Thanks to Page Object Pattern we don't have to think about it in our test steps, but only in our Page implementations. Screenshots helps a lot in diagnosing failures in TestCloud:</p>
<p><img class="aligncenter size-full wp-image-17881" src="{{ site.baseurl }}/assets/2017/06/TestCloud-screenshots.png" alt="Xamarin TestCloud - screenshots" width="800" height="478" /></p>
<p>Above test is failing when <em>Waiting for DetailsCommandLayout... </em>Thanks to screenshot, you can easily identify the line of code responsible for failure.</p>
<h3>Monitoring and Crash Reporting with HockeyApp and AppInsights</h3>
<p>A lot of people are using HockeyApp for crash reporting. Not many people are using it for application logging though. That's because HockeyApp does not provide a good way for searching logs. However, you can create an <a href="https://docs.microsoft.com/en-us/azure/application-insights/app-insights-hockeyapp-bridge-app">AppInsights bridge app</a> and stream all HockeyApp events to AppInsights.</p>
<p>AppInsights provides <a href="https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics">very powerful query explorer</a> to search through your logs.</p>
<p>By default logs are preserved for 3 months, but you can <a href="https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry">export them to storage account</a> and keep forever if you want.</p>
<p>What's more, you can create <a href="https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-power-bi">awesome PowerBI dashboards using data from AppInsights</a>.</p>
<h3>Xamarin Open Source plugins and libraries</h3>
<p>We saved a lot of time by using cross-platform Xamarin plugins:</p>
<ul>
<li><a href="https://github.com/jamesmontemagno/SettingsPlugin">XamSettings Plugin</a> (from James Montemagno) - it is an abstraction over native data storage (SharedPreferences for Android, NSUserDefaults for iOS) that allows you to store/access local data in shared code</li>
<li><a href="https://github.com/luberda-molinet/FFImageLoading">FFImageLoading</a> (from Daniel Luberda) - very powerful image library, it allows us to convert SVGs to native formats in runtime, in shared code</li>
<li><a href="http://www.oxyplot.org/">OxyPlot</a> (recommended by Frank Kruger) - awesome, powerful, cross-platform chart library used for metrics visualization</li>
</ul>
<p>Xamarin community is awesome. If you are building Xamarin apps, I strongly recommend you to join slack channel <a href="https://xamarinchat.slack.com">XamarinChat</a>. You can find there a lot of great developers who are willing to help. We learned about <a href="https://github.com/luberda-molinet/FFImageLoading">FFImageLoading</a> there. What's more, <a href="http://daniel-luberda.github.io/">Daniel Luberda</a> (<a href="https://github.com/luberda-molinet/FFImageLoading">FFImageLoading</a> top contributor) is very active there. One time, he fixed a bug in less than 6h after reporting it by us :)</p>
<h3>Summary</h3>
<p>I am really excited about this app. It is an awesome feeling to take an app from zero to <a href="https://youtu.be/YKK_XHMFE3U?t=594">//build keynote</a>. I am even more excited because there is a lot more to come. You can help us with that! If you have an idea about what should be added/changed/removed in Azure App go to <a href="https://aka.ms/azureapp/feedback">aka.ms/azureapp/feedback</a> and add or vote for a feature.</p>
<p>In meantime, get the app from App Store or Google Play, and let us know what you think!</p>
<p><a href="https://itunes.apple.com/us/app/microsoft-azure/id1219013620?ls=1&amp;mt=8"><img class="aligncenter size-full wp-image-18061" src="{{ site.baseurl }}/assets/2017/06/appstore.png" alt="" width="200" height="59" /></a></p>
<p><a href="https://play.google.com/store/apps/details?id=com.microsoft.azure"><img class="aligncenter size-full wp-image-18071" src="{{ site.baseurl }}/assets/2017/06/playstore.png" alt="" width="200" height="59" /></a></p>
<p>Check out me and <a href="https://twitter.com/jamesmontemagno">James Montemagno</a> chatting about the app on Xamarin Show:</p>
<p>
<iframe width="640" height="360" src="https://www.youtube.com/embed/7sR98Z0UnPU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>
<p>*This post was written in the clouds during my flight from Seattle to Frankfurt :)</p>

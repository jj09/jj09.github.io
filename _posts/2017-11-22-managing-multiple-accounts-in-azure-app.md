---
layout: post
title: Managing multiple accounts in Azure App
date: 2017-11-22 15:29:14.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- android
- AzureApp
- ios
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
  dsq_thread_id: '6303442000'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/managing-multiple-accounts-in-azure-app/"
---
<p>One of our <a href="https://feedback.azure.com/forums/568069-azure-mobile-app/filters/top">top user's feedback requests</a> was to enable <a href="https://feedback.azure.com/forums/568069-azure-mobile-app/suggestions/18825487-multiple-account-access">multiple account access</a> without singing out and signing in.</p>
<p>It is now available on latest <a href="https://aka.ms/azureapp/ios">iOS</a> and <a href="https://aka.ms/azureapp/android">Android</a> releases!</p>
<h3>Quick overview</h3>
<p><img class="aligncenter size-full wp-image-19333" src="{{ site.baseurl }}/assets/2017/11/AzureApp-MultiAccounts.gif" alt="Azure App - Multiple Accounts" width="376" height="668" /></p>
<p>You can see all your accounts in hamburger menu. You can add new account by tapping 'Add account'. To remove account you need to simply sign out.</p>
<h3>Limitations</h3>
<p><b>First limitation (AKA caveat):</b> when you are adding second live account you, you may run into the following screen during authentication with Active Directory:</p>
<p><img class="aligncenter wp-image-19343 size-full" src="{{ site.baseurl }}/assets/2017/11/AzureApp-alreadysignedin.png" alt="Azure App - already signed in" width="582" height="530" /></p>
<p>This is <a href="https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/issues/892">Active Directory limitation</a>. Just tap 'Sign out and sign in with a different account', and we will sign you in to another account <b>without signing you out from another</b>.</p>
<p><b>Second limitation:</b> you are not able to sign in into two accounts if they are associated with one email. Yes! One email can be used to sign in to more than 1 account. If you are seeing screen similar like below during authentication this is a case:</p>
<p><img class="aligncenter size-full wp-image-19383" src="{{ site.baseurl }}/assets/2017/11/AzureApp-MultiAccountsOneEmail-e1511392866455.png" alt="Azure App - Multi Accounts One Email" width="400" height="711" /></p>
<p>In this situation you need to sign out, and then sign in again choosing another account.</p>
<h3>Summary</h3>
<p>I personally love this feature as switching between my MSDN account and work account was a pain in the past. Now it's seamless.</p>
<p>We are still exploring possibility to enable users to sign in into two accounts tied to the same email. We are also looking at improvements around removing and adding accounts.</p>
<p>Do you have feedback? Let us know! You can ping <a href="https://twitter.com/JakubJedryszek">me</a> or <a href="https://twitter.com/AzureApp">our team</a> on twitter. You can also add or vote on existing ideas at <a href="https://aka.ms/azureapp/feedback">our User Voice</a>.</p>
<p>Happy Thanksgiving!</p>

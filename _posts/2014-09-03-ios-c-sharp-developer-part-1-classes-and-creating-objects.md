---
layout: post
title: 'iOS for C# Developer - part 1: Classes and creating objects'
date: 2014-09-03 12:58:21.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- ios
- iOS for C# Developer
- Objective-C
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
  dsq_thread_id: '2985146682'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/ios-c-sharp-developer-part-1-classes-and-creating-objects/"
---
<p>In <a title="iOS for C# Developer" href="http://jj09.net/tag/ios-for-c-developer/">this series</a> I would like to present an overview of differences and similarities in developing iOS and C# apps.</p>
<p>First part is about Object-Oriented features. If you are C# developer and you are starting with Objective-C, Object-Oriented terminology might be confusing.</p>
<h3>Interface</h3>
<p>In Objective-C, interface is a class declaration (not existing in C#). It is like header file in C++. It has even the same extension: <code>.h</code>. This is sample interface:</p>
<pre class="lang:objc decode:true ">@interface Example

+ (void)someStaticMethod;

- (NSInteger)someInstanceMethod:(BOOL)param1 calledWith:(NSInteger)num;

@end
</pre>
<p>Static (class) methods are distinguished by <code>+</code> sign. Instance method starts with <code>-</code> sign. Return types are in brackets. Parameters (brackets and name) are preceded by custom name. In class implementation only parameter name matters.</p>
<h3>Implementation</h3>
<p>In addition to interface (equivalent of class declaration), Objective-C classes have also implementation files with <code>.m</code> extension (equivalent of .cpp files in C++). Example implementation for previous interface (class declaration) can look like that:</p>
<pre class="lang:objc">@implementation Example

+ (void)someStaticMethod
{
  // implementation
}

- (NSInteger)someInstanceMethod:(BOOL)param1 calledWith:(NSInteger)num
{
  if(param1) {
    return num*2;
  } else {
    return num;
  }
}

@end
</pre>
<h3>Protocols</h3>
<p>Protocol is equivalent of interface in C#. This is sample protocol definition:</p>
<pre class="lang:objc">@protocol SampleProtocol
- (void)protocolMethod1;
- (void)protocolMethod2;
@end
</pre>
<p>To take advantage of this protocol in some class, it has to be stated in angled brackets, in the interface definition:</p>
<pre class="lang:objc">@interface Example : NSObject <sampleprotocol>
+ (void)someStaticMethod;
- (NSInteger)someInstanceMethod:(BOOL)param1 calledWith:(NSInteger)num;
@end
</sampleprotocol></pre>
<p>Then, its methods have to be implemented in the implementation file:</p>
<pre class="lang:objc">@implementation Example 

+ (void)someStaticMethod 
{ 
  // implementation 
} 

- (NSInteger)someInstanceMethod:(BOOL)param1 calledWith:(NSInteger)num 
{ 
  if(param1) { 
    return num*2; 
  } else { 
    return num; 
  } 
} 

- (void)protocolMethod1 
{ 
  // implementation 
} 

- (void)protocolMethod2 
{ 
  // implementation 
} 

@end
</pre>
<p>There are two types of methods in protocol:</p>
<ul>
<li>required (default)</li>
<li>optional</li>
</ul>
<p>In previous protocol, both methods are required, because it is a default mode. This means, both has to be implemented in the class that use the protocol. In order to make second method optional, keyword <code>@optional</code> has to be used:</p>
<pre class="lang:objc">@protocol SampleProtocol

- (void)protocolMethod1;

@optional
- (void)protocolMethod2;

@end
</pre>
<p>All methods declared after <code>@optional</code> keyword are optional. In order to declare required method after that, <code>@required</code> keyword has to be used:</p>
<pre class="lang:objc">@protocol SampleProtocol

- (void)protocolMethod1;  // required method

@optional
- (void)protocolMethod2;  // optional method
- (void)protocolMethod3;  // optional method

@required
- (void)protocolMethod4;  // required method

@end
</pre>
<h3>Instantiating objects</h3>
<p>Creating instance of object has two steps: allocation and initialization. To create instance of <code>Example</code> class defined above, message passing syntax is used:</p>
<pre class="lang:objc">Example *obj = [[Example alloc] init];</pre>
<p>Shortcut for above object creation:</p>
<pre class="lang:objc">Example *obj = [Example new];</pre>
<p>When the class has a constructor with parameters, e.g.:</p>
<pre class="lang:objc">@interface Example : NSObject {
  NSInteger *sampleProperty;
}
- (id) initWithParam:param;
@end

@implementation Example

- (id) initWithParam:(NSInteger)param
{
  self = [super init];
  if (self) {
    self.sampleProperty = param;
  }
  return self;
}

@end</pre>
<p>Initialization looks as follows:</p>
<pre class="lang:objc">Example *obj = [Example initWithParam:25];</pre>
<h3>Summary</h3>
<ul>
<li>Interface - class declaration</li>
<li>Implementation - class body (implementation of declared methods in class interface)</li>
<li>Protocol - the same construct as interface in C#</li>
<li>Object creation: <code>Example *obj = [[Example alloc] init];</code></li>
</ul>

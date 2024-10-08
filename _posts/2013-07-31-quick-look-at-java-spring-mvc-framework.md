---
layout: post
title: Quick look at Java Spring MVC framework
date: 2013-07-31 09:49:12.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- framework
- Java
- MVC
- Spring MVC
meta:
  _yoast_wpseo_linkdex: '91'
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _yoast_wpseo_focuskw: Spring MVC
  _yoast_wpseo_metadesc: Overview of Spring MVC framework. Spring MVC vs. ASP.NET
    MVC vs. Rails
  _syntaxhighlighter_encoded: '1'
  dsq_thread_id: '1551553597'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/quick-look-at-java-spring-mvc-framework/"
---
<p>Java software market is still bigger than .NET. Many times, when I heard that some friend on mine is working as Java Web Developer, he is using Spring MVC framework. Finally I decided to look at this (most popular?) Java Web Framework.</p>

<p>I started with <a href="http://www.pluralsight.com/">Pluralsight.net</a> tutorials: <a href="http://pluralsight.com/training/courses/TableOfContents?courseName=springmvc-intro">Introduction to Spring MVC</a> and <a href="http://pluralsight.com/training/courses/TableOfContents?courseName=spring-jpa-hibernate">Spring with JPA and Hibernate</a>.</p>

<p>First surprise for me was a lot of xml based configuration, which needs to be written by developer. E.g. we need to configure which class is controller by declaring its path in xml file (servlet-config.xml). For some other elements we need to provide long uris as packages' names. So easy to misspell. This is 'configuration over convention', instead of 'convention over configuration' as it is in Ruby on Rails or ASP.NET MVC.</p>

<p>As an example, look at this piece of xml, which is needed to handle JSON and XML requests (all written by hand):

{% highlight xml %}
<bean class="org.springframework.web.servlet.view.ContentNegotiatingViewResolver">
		<property name="order" value="1" />
		<property name="contentNegotiationManager">
			<bean class="org.springframework.web.accept.ContentNegotiationManager">
				<constructor-arg>
					<bean class="org.springframework.web.accept.PathExtensionContentNegotiationStrategy">
						<constructor-arg>
							<map>
								<entry key="json" value="application/json" />
								<entry key="xml" value="application/xml" />
							</map>
						</constructor-arg>
					</bean>
				</constructor-arg>
			</bean>
		</property></p>
		<property name="defaultViews">
			<list>
				<bean class="org.springframework.web.servlet.view.json.MappingJacksonJsonView" />
				<bean class="org.springframework.web.servlet.view.xml.MarshallingView">
					<constructor-arg>
						<bean class="org.springframework.oxm.xstream.XStreamMarshaller">
							<property name="autodetectAnnotations" value="true" />
						</bean>
					</constructor-arg>
				</bean>
			</list>
		</property>
	</bean>
{% endhighlight %}

<p>Going back to controller: besides its configuration in XML file, we need to add annotation <em>@Controller</em> on its class and <em>@RequestMapping</em> on methods (no default routing). Additionally we always need to return the name of view (instead of some default value). Here is a sample controller with one action:</p>

{% highlight java %}
@Controller
public class HelloWorldController {
    @RequestMapping("/helloWorld")
    public String helloWorld(Model model) {
        model.addAttribute("message", "Hello World!");
        return "helloWorld";
    }
}
{% endhighlight %}

<p>Above code will return the view <em>helloWorld.jsp</em> (according to convention, located in <em>webapp/WEB-INF/jsp/</em> directory):</p>

{% highlight html %}
<!DOCTYPE html>
<html>
    <head></head>
    <body>
        Message: ${message}
    </body>
</html>
{% endhighlight %}

<p>The result should looks like that:</p>

<p><img src="{{ site.baseurl }}/assets/2013/07/SpringMVCHelloWrold.png" alt="Spring MVC Hello World" width="167" height="31" class="aligncenter size-full wp-image-537" /></p>

<p>Connecting application with database is not easier. Adding dependencies and writing code to make Hibernate working with the app took 1h(!) in Pluralsight tutorial (<a href="http://pluralsight.com/training/courses/TableOfContents?courseName=spring-jpa-hibernate">Spring with JPA and Hibernate</a>). It is over 50 lines of xml. Additionally as we know - it is very easy to make a mistake during writing xml. In ASP.NET MVC it can be done automatically (eventually we can change data source by specifying connection string). I didn't find easier way to do that (in Spring). Of course we can use copy/paste method and just set some properties, but...where is code generation for that?</p>

<p>After all, I would like to notice how big step was made by other MVC Web Frameworks like Rails, Django or ASP.NET MVC. Lot of stuff, which has to be written by hand in Spring, is already implemented under framework layer (in Rails, Django and ASP.NET MVC). However Spring MVC was also big step ahead, when it was created in 2002. In <a href="http://www.youtube.com/watch?v=FQp8lEp8uro">this video</a> people are explaining that (e.g. because of Spring they do not need to rewrite lots of boilerplate code anymore). </p>

<p>I wonder whether next version of Spring MVC will have more 'conventions' and default configurations. It will make the framework more developer friendly and easier to maintain.</p>

<p>If you want to start with Spring MVC i recommend you to start with <a href="http://www.pluralsight.com/">Pluralsight.net</a> tutorials: <a href="http://pluralsight.com/training/courses/TableOfContents?courseName=springmvc-intro">Introduction to Spring MVC</a> and <a href="http://pluralsight.com/training/courses/TableOfContents?courseName=spring-jpa-hibernate">Spring with JPA and Hibernate</a>. You can also find <a href="http://www.springsource.org/tutorials">this website</a> useful, as well as <a href="http://static.springsource.org/spring/docs/3.0.x/spring-framework-reference/html/">Spring Framework Reference Documentation</a>. I didn't read any book, but I found those two most often recommended: <a href="https://amzn.to/3JF8mc7">Spring Recipes</a> and <a href="https://amzn.to/40r9UgG">Spring in Action</a>.</p>

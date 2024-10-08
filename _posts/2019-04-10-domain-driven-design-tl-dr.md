---
layout: post
title: Domain-Driven Design - tl;dr
date: 2019-04-10 11:20:16.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- DDD
- Domain-Driven Design
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
  dsq_thread_id: '7349090429'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/domain-driven-design-tl-dr/"
---
<p><img class="aligncenter size-full wp-image-19707" src="{{ site.baseurl }}/assets/2019/04/ddd-diagram-example.png" alt="Domain Driven Design" width="581" height="409" /></p>
<p>After hearing about Aggregates and Bounded Contexts over, and over again, I decided to check out what Domain-Driven Design is all about. There is a ton of DDD resources on the Internet, but this blog post is for my personal reference. I am publishing it so I can google it, and maybe you find it useful as well. This post is about what DDD is, and how it can help you to write better code.</p>
<h3>What is DDD?</h3>
<p>According to <a href="https://en.wikipedia.org/wiki/Domain-driven_design">Wikipedia</a>:</p>
<blockquote><p>Domain-driven design (DDD) is an approach to software development for complex needs by connecting the implementation to an evolving model. The premise of domain-driven design is the following:</p>
<ol>
<li>placing the project's primary focus on the core domain and domain logic;</li>
<li>basing complex designs on a model of the domain;</li>
<li>initiating a creative collaboration between technical and domain experts to iteratively refine a conceptual model that addresses particular domain problems.</li>
</ol>
</blockquote>
<p>More pragmatic (and ignorant) definition: DDD is software development approach that focus on business processes over implementation details. This allows developers to work with business people more effectively. It also makes code more maintainable and extendable.</p>
<p>Most important DDD terms (buzzwords):</p>
<ul>
<li>Ubiquitous Language - using business terms for naming classes, methods and variables</li>
<li>Domain - functionality of the system</li>
<li>Bounded Context - components used to deliver a functionality (AKA domains)</li>
<li>Value Object - simple, immutable class representing some business term</li>
<li>Entity - class with unique identifier, usually used to represent persistent data</li>
<li>Aggregate - group of entities</li>
<li>Repository - class used to save and retrieve aggregate (AKA save/retrieve data to/from database)</li>
<li>Application Service - your Domain(s) communication layer</li>
<li>Anti-corruption layer - layer for interaction with external (or legacy) system</li>
<li><a href="https://martinfowler.com/bliki/CQRS.html">CQRS (Command Query Responsibility Segregation)</a> - separates querying for data from modifying data</li>
<li><a href="https://martinfowler.com/eaaDev/EventSourcing.html">Event Sourcing</a> - storing changes to application state as a list of events, which allows to invoke and process events in producer/consumer fashion</li>
</ul>
<h3>Resources to learn about Domain-Driven Design</h3>
<p>There are two DDD bibles: <a href="https://amzn.to/2rR3Wrl">Blue Book</a> and <a href="https://amzn.to/2SqKOfa">Red Book</a>. I've been told to do not read <a href="https://amzn.to/2rR3Wrl">Blue Book</a> as first introduction to DDD, because it's very "heavy" and hard to understand. People were right. I would also add: it's not very well written (shoot me for criticizing DDD God AKA Eric Evans).</p>
<p>List of recommended resources, sorted in order that I would recommend to follow if you are new to DDD. I strongly recommend positions in bold!</p>
<ul>
<li><a href="https://app.pluralsight.com/library/courses/domain-driven-design-fundamentals">Domain Driven Design Fundamentals (Pluralsight)</a> - this will give you an idea what DDD is, perfect to watch during short flight in 2x speed</li>
<li><b><a href="https://amzn.to/2BABNZY">Domain-Driven Design Distilled (Vaughn Vernon)</a> - overview of key ideas from <a href="https://amzn.to/2rR3Wrl">Blue Book</a>, this will help you to put all, high-level pieces together</b></li>
<li><b><a href="https://www.infoq.com/minibooks/domain-driven-design-quickly">Domain Driven Design Quickly</a> (thanks <a href="https://mfranc.com/">Michal Franc</a>) - similar to DDD Distilled, but use even more systematic approach to outline DDD concepts</b></li>
<li><b><a href="https://app.pluralsight.com/library/courses/domain-driven-design-in-practice">Domain-Driven Design in Practice (Pluralsight)</a> - this course shows how to actually use DDD in a project; course author <a href="https://app.pluralsight.com/profile/author/vladimir-khorikov">Vladimir Khorikov</a> has a blog <a href="https://enterprisecraftsmanship.com/">Enterprise Craftsmanship</a>, which is very good source of DDD and general Software Development knowledge</b></li>
<li><a href="https://www.pluralsight.com/courses/domain-driven-design-legacy-projects">Domain-Driven Design: Working with Legacy Projects (Pluralsight)</a> - another course from <a href="https://app.pluralsight.com/profile/author/vladimir-khorikov">Vladimir Khorikov</a> that is a nice demonstration of transforming legacy projects into DDD-friendly architecture</li>
<li><a href="https://amzn.to/2SqKOfa">Implementing DDD "Red Book" (Vaughn Vernon)</a> - comprehensive overview of DDD</li>
<li><a href="https://amzn.to/2rR3Wrl">Domain-Driven Design "Blue Book" (Eric Evans)</a> - the Bible of DDD, use it as a reference rather than reading from back to back</li>
</ul>
<p>Notice that I placed <a href="https://amzn.to/2rR3Wrl">Blue Book</a> at the end. It's hard to absorb. It also suffers from low knowledge/pages ratio.</p>
<p>There is also <a href="https://app.pluralsight.com/paths/skills/domain-driven-design"> Domain-Driven Design path</a> on Pluralsight that has nice set of courses around DDD and software design.</p>
<h3>My thoughts on DDD</h3>
<p>Before diving into DDD I was expecting to learn about something new and revolutionary. After reading about Ubiquitous Language, Aggregates and Bounded Context I still didn't see much difference between DDD and good, <a href="https://en.wikipedia.org/wiki/SOLID">SOLID</a> software design. It feels like DDD is mostly about good object-oriented design presented in particular, formalized way with specific buzzwords (aggregate, bounded context, etc.). In Uncle Bob's <a href="https://amzn.to/2LxBMuv">Agile Principles, Patterns, and Practices in C#</a>, there is <a href="http://cleancodejava.com/uncle-bob-payroll-case-study-full-implementation/">the Payroll Case Study</a> example that is following clean code, good design and implementation practices. If you were put that example into DDD book...it would fit. If you take examples from DDD books and put it into Uncle Bob's book...it would fit fine as well.</p>
<p>There are however, some new concepts introduced by DDD. Such as <a href="https://deviq.com/repository-pattern/">Repository pattern</a>, <a href="https://martinfowler.com/bliki/CQRS.html">CQRS</a> or <a href="https://martinfowler.com/eaaDev/EventSourcing.html">Event Sourcing</a>. Are last two actually DDD? Or they are just related to DDD?</p>
<p>DDD is also enforcing designing system around business domain, not around, e.g. database. That is usually a case when designing architecture from scratch quickly. As 99% of apps are CRUDs, ending up with database driven architectures would be natural. You usually start with file-&gt;new project, and go from there. This is not a problem for small apps, but might strike later when evolving the app. DDD solves that problem.</p>
<p>If you are familiar with <a href="https://amzn.to/2BBzG84">Clean Code</a> and <a href="https://en.wikipedia.org/wiki/SOLID">SOLID</a> design as presented in <a href="https://amzn.to/2LxBMuv">Agile Principles, Patterns, and Practices in C#</a> then DDD does not bring much new concepts to the table. It may make you think more from a business perspective, and consider using new patterns (<a href="https://deviq.com/repository-pattern/">Repository pattern</a>, <a href="https://martinfowler.com/bliki/CQRS.html">CQRS</a> or <a href="https://martinfowler.com/eaaDev/EventSourcing.html">Event Sourcing</a>) though.</p>
<p>It's worth to notice that even if you look at <a href="https://app.pluralsight.com/paths/skills/domain-driven-design">Domain-Driven Design path</a> on Pluralsight, there are non-DDD courses about good/clean design as part of the path. Thus, good design is prerequisite of DDD. On top of that we have mentioned earlier buzzwords, <a href="https://martinfowler.com/bliki/CQRS.html">CQRS</a> and <a href="https://martinfowler.com/eaaDev/EventSourcing.html">Event Sourcing</a>.</p>
<p>Going back to DDD terms (AKA buzzwords), they could be also summarized as follows:</p>
<ul>
<li>Ubiquitous Language - use meaningful names for classes, methods and variables</li>
<li>Domain - be aware what problem you are solving</li>
<li>Bounded Context - group objects that depends on each other</li>
<li>Value Object - simple, immutable class</li>
<li>Entity - class with unique identifier, usually used to represent persistent data</li>
<li>Aggregate - group of related entities</li>
<li>Repository - facade over your persistence layer to make it implementation agnostic</li>
<li>Application Service - your system's API</li>
<li>Anti-corruption layer - layer for interaction with external system</li>
<li><a href="https://martinfowler.com/bliki/CQRS.html">CQRS (Command Query Responsibility Segregation)</a> - separates querying for data and modifying data</li>
<li><a href="https://martinfowler.com/eaaDev/EventSourcing.html">Event Sourcing</a> - storing changes to application state as a list of events, which allows to invoke and process events in producer/consumer fashion</li>
</ul>
<p>What DDD enforces from the beginning is layered architecture that may not always be needed. Should you follow DDD in your projects? The answer is, as always, "it depends". There are some good ideas there, but being over obsessed with favoring DDD in your design decisions over pragmatism will lead to over-engineering.</p>
<p>After TDD and BDD there is DDD. Should you use DDD in all your projects? No. It's just a way to design software. Also: using DDD does not mean that you need to use all patterns from <a href="https://amzn.to/2rR3Wrl">Blue Book</a> and <a href="https://amzn.to/2SqKOfa">Red Book</a>.</p>
<p>It seems like DDD should definitely help in long term, but over-engineering (with <a href="https://martinfowler.com/bliki/CQRS.html">CQRS</a> and <a href="https://martinfowler.com/eaaDev/EventSourcing.html">Event Sourcing</a>) may unnecessary complicate things. Actually, I should say: writing <a href="https://en.wikipedia.org/wiki/SOLID">SOLID</a> code would help you...and here we are again: is DDD really something different than just good software design?</p>

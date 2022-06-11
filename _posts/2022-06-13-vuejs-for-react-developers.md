---
layout: post
title: Vue.js for React Developers
categories:
- javascript
permalink: "/vue-for-react-developers/"
---

It's been a while since I learned “yet another” JavaScript framework. I recently joined the [Super.Events](https://super.events) team at Meta and the Super web app is written in [Vue.js](https://vuejs.org/).

I’ve been working with [Knockout](https://jj09.net/ndc-london-2016-azure-portal-and-recommended-talks/), [Angular](https://jj09.net/tdd-with-typescript-angularjs-and-node-js/), [React](https://jj09.net/cognitive-search-azure-search-with-ai/) and [Aurelia](https://jj09.net/strange-loop-and-ncdevcon/) in the past. Vue has a lot of similarities with pretty much all of them. It’s like an intersection of Angular and React. This blog post is a short overview of gotchas and differences between Vue and other JS frameworks.

<h2>Basics</h2>
I’ve been doing development in VSCode, with the [Vetur extension](https://marketplace.visualstudio.com/items?itemName=octref.vetur). It’s very useful because vue is using Single-File Components. Vue components have <em>.vue</em> extension and following structure:

{% highlight vue %}
<template>
<!-- html –>
</template>
<script>
// JS code
</script>
<style>
/ * css styles */
</style>
{% endhighlight %}

You can generate a Vue app with [Vue CLI](https://cli.vuejs.org/). It’s useful for quickly generating app skeletons, and also provides out of box bundling and minification for production.

<h2>Key things to learn</h2>

* Vue has [props](https://vuejs.org/tutorial/#step-12) and state (like React)
* Vue allows to create [components](https://vuejs.org/tutorial/#step-11) and reference them similarly to React
* [​​Vuex](https://vuex.vuejs.org/) is a store like [Redux](https://redux.js.org/)
* Vue router is very similar to Angular router
* Dynamic text uses mustaches syntax: _<div>Hello, \{\{ name \}\}</div>_ (almost like React but with double curly braces)
* There is [options API and composition API](https://fjolt.com/article/vue-composition-api-vs-options-api) - the best explanation of differences is in [https://vuejs.org/tutorial/](https://vuejs.org/tutorial/) (you can switch code samples between options and composition API) and in [Vue JS 3 Tutorial for Beginners](https://www.youtube.com/playlist?list=PL4cUxeGkcC9hYYGbV60Vq3IXYNfDk8At1) ([part1](https://www.youtube.com/watch?v=V-kxBWcPJfo&list=PL4cUxeGkcC9hYYGbV60Vq3IXYNfDk8At1&index=10), [part2](https://www.youtube.com/watch?v=V-kxBWcPJfo&list=PL4cUxeGkcC9hYYGbV60Vq3IXYNfDk8At1&index=10))
* To bind variable to component use `v-bind:variable` or `:variable` ([example](https://vuejs.org/tutorial/#step-3))
* For two way bindings use `v-model` ([example](https://vuejs.org/tutorial/#step-5))
* For event bindings use `v-on` or `@` ([example](https://vuejs.org/tutorial/#step-4))
* You can do conditional rendering with `v-if` directive ([example](https://vuejs.org/tutorial/#step-6))
* Directive for iterating thru list: `v-for` ([example](https://vuejs.org/tutorial/#step-7))
* Other useful things:
    * [Computeds](https://vuejs.org/tutorial/#step-8) - changes when underlying variables change, similar to Knockout `ko.computed`
    * [Refs](https://vuejs.org/tutorial/#step-9) - allows to reference DOM element and manipulate it directly
    * [Watchers](https://vuejs.org/tutorial/#step-10) - allows to subscribe to variable changes, similar to Knockout subscriptions
    * [Emits](https://vuejs.org/tutorial/#step-13) - you can emit events with `this.$emit(‘my event’)`

<h2>Resources</h2>

* **[Vue JS Crash Course](https://www.youtube.com/watch?v=qZXt1Aom3Cs) - awesome (the best) overview of Vue**
* [Vuex Tutorial](https://www.youtube.com/playlist?list=PL4cUxeGkcC9i371QO_Rtkl26MwtiJ30P2) - great overview of Vuex store
* [Differences between Vue 2 vs Vue 3](https://javascript.plainenglish.io/differences-between-vue-2-and-vue-3-ee627e2c83a8) - the most recent version of vue is 3, but a lot of apps are still written in vue 2
* [Vue JS 3 Tutorial for Beginners](https://www.youtube.com/playlist?list=PL4cUxeGkcC9hYYGbV60Vq3IXYNfDk8At1) - more comprehensive overview of all vue features, if you watched above, I recommend especially the videos about composition API, which is specific for Vue 3:
    * [Vue JS 3 Tutorial for Beginners #10 - The Composition API (part 1)](https://www.youtube.com/watch?v=V-kxBWcPJfo&list=PL4cUxeGkcC9hYYGbV60Vq3IXYNfDk8At1&index=10)
    * [Vue JS 3 Tutorial for Beginners #11 - The Composition API (part 2)](https://www.youtube.com/watch?v=0FwBjPeLqQ8&list=PL4cUxeGkcC9hYYGbV60Vq3IXYNfDk8At1&index=11)
* [Official vue.js tutorial](https://vuejs.org/tutorial/) - quick overview of all vue features (recommended after going through tutorials to refresh your knowledge)
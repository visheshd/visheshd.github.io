---
layout: post
title: Startup friendly analytics, finally! - Heap
type: post
published: true
excerpt: "If you're a preliminary Google Analytics users you will love this. In fact, you might even question why is Google 
Analytics still such a crap product."
comments: true
tags: [google analytics, heap analytics, analytics]
---

<figure>
	<img src="../images/heap-logo.jpg">
</figure>

If you're a preliminary Google Analytics users you will love this. In fact, you might even question why is Google 
Analytics still such a crap product.

There are many alternatives out there with Mixpanel, Kissmetrics and Heap Analytics.  

With Heap, the biggest win for me is you don't really need to code to define an event. You simply use their visualizer to open 
your page and define any went on any element on your page.

Let's look at how easy it is to set up.

## 1. Sign up

## 2. To get started with Heap, paste the code snippet given to you after signup to your website's closing </head> tag:
It should look something like this.
{% highlight html javascript %}
<script type="text/javascript">
	window.heap=window.heap||[],heap.load=function(e,t){window.heap.appid=e,window.heap.config=t=t||{};var r=t.forceSSL||"https:"===document.location.protocol,a=document.createElement("script");a.type="text/javascript",a.async=!0,a.src=(r?"https:":"http:")+"//cdn.heapanalytics.com/js/heap-"+e+".js";var n=document.getElementsByTagName("script")[0];n.parentNode.insertBefore(a,n);for(var o=function(e){return function(){heap.push([e].concat(Array.prototype.slice.call(arguments,0)))}},p=["addEventProperties","addUserProperties","clearEventProperties","identify","removeEventProperty","setEventProperties","track","unsetEventProperty"],c=0;c<p.length;c++)heap[p[c]]=o(p[c])};
	heap.load("2675588232");
</script>
{% endhighlight %}

## 3. Use their visualizer to actually go to your site and define events.
<figure>
	<img src="../images/heap-visualizer.png">
</figure>

## 4. On your site select the element you want to add the event to
<figure>
	<img src="../images/heap-event-1.png">
</figure>

## 5. Define the event
<figure>
	<img src="../images/heap-event-2.png">
</figure>

## 6. Done and you can now analyze the funnel. It is really that simple. 
<figure>
	<img src="../images/heap-funnel.png">
</figure>

Especially if you want to test out something new and validate things, this is great.

## Nerd talk
No more adding Javascript for event definition. Granted it uses CSS selectors which might break if there are changes in
those. But for startups that want to move fast; Heap's simple approach to defining events is priceless.

I am excited about the possibilities and eager to know how it will perform as a tool at scale. If you have experience 
with  other tools or Heap. I would love to know about it.

Know more about how it compares with Google Analytics and others, [here](https://heapanalytics.com/compare/heap-vs-google-analytics).


---
layout: post
title: Node live - Bengaluru
excerpt: "The node event at Wipro Bengaluru sucked, is an understatement.  With presenters not showing on time; to some not 
showing up at all."
type: post
published: true
tags: [npm, node, wipro, cto]
comments: true
---

<figure>
	<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/db/Npm-logo.svg/2000px-Npm-logo.svg.png">
</figure>
The node event at Wipro Bengaluru sucked, is an understatement.  With presenters not showing on time; to some not 
showing up at all. It was frustrating to travel to node/npm branded event only to find out they were hardly involved. 
Very surprised they would do that. But in this age where every one wants to be an instant community and a name people 
should know. Everything is fair game. Including short changing your attendees. Even the free booze by Wipro couldn't help.

The consolation was the bits of new information that I did get to learn.

##npm and the Node Foundation is doing a ton of work

They are doing a lot of work in promoting npm and node. Checkout the presentation by [Ashley Williams](http://ashleygwilliams.github.io/node-live/#1).

##npm goodies that I never used

```
npm init --yes == Assumes default

npm i -S // same as --save
npm i -D // same as --save-dev

npm3 = new release, installs dependency on the top if there is none for a particular package

npm ls --depth=0 //Primary dependency list
```

### Install offline
```
npm install --cache-min 9999 // Use this to install stuff from from global cache
```

Or better yet, as suggested by Ashley, alias it:
```
alias nci=npm install --cache-min 9999
```

### Pack and install using a tarball
```
npm pack //Inside the npm module source code to generate a tar ball

npm install my-pkg.tgz //Installing from a tarball
```

### Lock down for production
npm shrinkwrap

## KrakenJS
Out of the box security configurations and modules.
Support for local and custom npm repository. And yet another framework to explore. Learn more about it at [krakenjs.com](http://krakenjs.com/)


## JS closures -- talk
A fundamental JavaScript topic that elludes most JS devs. It was good refresher

var x = returnAClosure;

x needs to then be nullified for all the closure related memory to be released

## Some more tech and tools
At the very end, Wipro decided they needed to vomit all they were doing in open source to promote themselves and dived 
into a ridiculous talk that had nothing to with node at all.

Things that they are playing with that could be worth looking into though are:

1. Apache Kafka
2. Storm 
3. ZettaJS - IoT




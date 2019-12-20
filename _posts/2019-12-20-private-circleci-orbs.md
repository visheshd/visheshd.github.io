---
layout: post
title: Private CircleCI Orb
type: post
published: true
excerpt: "How do I create a private circleci orb?"
comments: true
tags: [circleci, orb]
---

# How do I create a private circleci orb?

Well turns out there isn't a way to do this. It's such an obvious usecase that they should!

The next best thingk you can do is to have it be public but unlisted. Here is how you can do that.

```
circleci orb unlist <namespace>/<orb> <true|false>
```

[Link to the docs.](https://circleci-public.github.io/circleci-cli/circleci_orb_unlist.html)
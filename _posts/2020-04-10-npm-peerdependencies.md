---
layout: post
title: peerDependencies Can't resolve module
type: post
published: true
excerpt: "The right way to use peerDependencies"
comments: true
tags: [npm, peerdependencies, dependencies]
---

I'm not gonna talk about what the [different types of dependencies](https://dev.to/yvonnickfrin/how-to-handle-peer-dependencies-when-developing-modules-18fa). 

If there is a dependency that is a library that you are using to build another library. For example you are building a new ORM that required mongoose As a dependency. Now if the installing app that is using any of the mongoose API directly then they are going to be installing the mongoose library themselves together with your library which will also bring in the mongoose dependency. Most cases this is not an issue but if npm Is not able to resolve the dependency conflict then you might end up with issues arising from conflicting versions of mongoose.

The fixe os to simply in your ORM define mongoose as a peer dependency. But how do you make sure that mongoose actually gets resolved while developing and testing your ORM.

It's pretty straightforward in your package.json 

```javascript

peerDependencies {
  mongoose: "^5.9.7"
}

devDependencies {
  mongoose: "5.9.7"
}

```

So add it also as a dev dependency. Tedious yes, could be simpler probably. 
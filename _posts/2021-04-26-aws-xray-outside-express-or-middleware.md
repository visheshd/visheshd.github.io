---
layout: post
title: AWS Xray outside express or without a supported middleware
type: post
published: true
excerpt: "Setting up AWS Xray"
comments: true
tags: ["aws", "aws-xray", "xray", "nodejs"]
---

Manual tracing with Xray can be cumbersome and you don't really need it. Here is how you can setup automatic mode up without a middleware or outside express.

So if you have a dockerized nodejs service running you can change the entrypoint of your service to something like this.

```typescript
import AWSXRay from 'aws-xray-sdk-core';

AWSXRay.captureAWS(require('aws-sdk'));
AWSXRay.enableAutomaticMode();

var ns = AWSXRay.getNamespace();

ns.run(async function() {
  var segment = new AWSXRay.Segment('Service Name');
  AWSXRay.setSegment(segment);

  /// Call your service code or entrypoint here
  segment.close();
});

```
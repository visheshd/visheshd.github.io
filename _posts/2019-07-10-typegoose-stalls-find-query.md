---
layout: post
title: Typegoose stuck on find* query
type: post
published: true
excerpt: "Been playing with typegoose lately. The library has it's quirks including this weird issue of queries stalling."
comments: true
tags: [typegoose, mongoose, node, serverless]
---

Been playing with typegoose lately. The library has it's quirks including this weird issue of queries stalling. 

There are a couple of open issues highlighting the issue as I write this. For all methods like find, findOne etc the execution was simply stuck at the method call.

Essentially the problem is tha typgoose ships with mongoose as a strict dependency and [expects you to pass your instance of mongoose or mongoose connection](https://github.com/szokodiakos/typegoose#methods) as an argument to `getModelForClass`.

I ended up doing that but it took forever to debug because the connection I passed wasn't active. To make things easier to debug I wrote a small wrapper around `getModelForClass`.

```javascript

import { Typegoose } from 'typegoose';
import { Database } from '@config/database';
import { log } from '@config/logger';


export async function getModel<T extends Typegoose>(Clazz: new (...args: any) => T) {
  const connection = await new Database().connect();

  if (connection.readyState !== 1) {
    throw new Error(`Can't get model as the database connection is not active.`);
  }

  const Model = new Clazz().getModelForClass(Clazz, {
    existingConnection: connection,
    schemaOptions: {
      timestamps: true,
    },
  });

  return Model;
}
```

Typegoose is a quirky and some of that comes from the limitations of typescript reflection system itself. Hope this was of help.

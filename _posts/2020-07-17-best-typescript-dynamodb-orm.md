---
layout: post
title: The best typescript dynamodb ORM
type: post
published: true
excerpt: "In the last month and a half I have looked at multiple DynamoDB ORMs; Dyngoose is by far the best."
comments: true
tags: [dynamo, dynamodb, typescript, orm, nodejs]
---

Selecting an ORM is a tough call because it cuts through pretty much your entire application. You want to make sure that what you end up picking something that is not only easy to use but also allows you to go native if and when needed.

The three that were serious contenders included
1. [AWS data mapper](https://github.com/awslabs/dynamodb-data-mapper-js) , I was really surprised at their release rate 
2. [dynamoose](https://dynamoosejs.com/), the syntax is too verbose
3. [dyngoose](https://github.com/benhutchins/dyngoose)

Others simply were not well typed. Dyngoose beats them hands down in almost all aspects. And is pretty well maintained by [Ben](https://github.com/benhutchins) who is pretty responsive. 

## Typed models
Dyngoose allows you to define your models as a typescript class and you can annotate your attributes using decorators. I really like this approach because I can then use something like type-graphql to specify my graphql schema and everything is nicely packaged as a single source of truth.

```javascript

import { Dyngoose } from 'dyngoose';
import { GqlField, GqlType } from '@common/types/typegraphql-aliases';

import { Status, Type } from './enums';

@Dyngoose.$Table({
  name: `${process.env.STAGE}_message`,
  encrypted: false,
  stream: true,
})
@GqlType()
export class TypedModel extends Dyngoose.Table {
  @GqlField()
  @Dyngoose.Attribute.String({ default: () => 'Missing Hash' })
  hash: string;

  @GqlField()
  @Dyngoose.Attribute.Number({ default: () => Status.IDLE })
  status: Status;

  @GqlField()
  @Dyngoose.Attribute.String()
  type: Type;
}

```

Note: GqlField and GqlType are aliases for classes from type-graphql

There other features like batch optimizations, selective updates to prevent wasteful uploading of unchanged values and DynamoDB Accelerator (DAX) and Amazon X-Ray support make it a very obvious choice.

It allows you flexibility to go native with methods `toDynamo` and `fromDynamo` to hook into.

What is your choice of DynamoDB ORM and why?


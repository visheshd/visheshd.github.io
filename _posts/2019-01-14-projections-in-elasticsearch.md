---
layout: post
title: Query or Field Projections in ElasticSearch
type: post
published: true
excerpt: "Don't return the entire indexed document to the client when you don't need to."
comments: true
tags: [elasticsearch, search index, query performance]
---

I am currently working on project that involves dealing with massive amounts of data. To a point where we are seeing performance issues on the client.

One of the issues we've identified that can be improved includes what we send to the UI. We are indexing public documents and web pages for certain industry. For a job like this you don't just store data that you show but also index analytical data. Also, our data model is pretty big; most users will almost never try to see all the fields together.

To reduce the size of the network response we have started sending only a subset of fields. It's fairly standard to use query projections or field projections in databases but doing so with a search index is fairly easy yet not so common. ElasticSearch chooses to refer this as [`Source Filtering`](https://www.elastic.co/guide/en/elasticsearch/reference/7.5/search-request-body.html#request-body-search-source-filtering).

You can simply pass the field(s) you want to returned in the query as `_source`. 

Turn off getting the stored document all together by passing `false`

```
GET /_search
{
    "_source": false,
    "query" : {
        "term" : ...
    }
}
```

Get a subset of fields using a wildcard for example if there is a field with nested fields called `address`

```
GET /_search
{
    "_source": "address.*",
    "query" : {
        "term" : ...
    }
}
```

Get a subset of explicitly named fields by sending in the exact names

```
GET /_search
{
    "_source": [ "name", "address", "bio"],
    "query" : {
        "term" : ...
    }
}
```

If you want to do fine tune further there is a way to pass both include and exclude list 

```
GET /_search
{
    "_source": {
      "includes": [ "name", "address", "bio"],
      "excludes": [ "email"]
    }
    "query" : {
        "term" : ...
    }
}
```

It was easy enough to figure out but more importantly the lesson was to never forget to pay attention to what you are sending to the client.
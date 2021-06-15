---
layout: post
title: Generating GraphQL Docs
type: post
published: true
excerpt: "It is super easy to generate GraphQL docs using Docusaurus"
comments: true
tags: ["graphql", "graphql docs", "documentation", "typescript"]
---

To generate documentation for the GraphQL api the schema needs to have comments or description. Here is an example of how you could add a comment.

```gql

"""
Location information for an actor
"""
type ActorLocation {
  """
  City
  """
  city: String

  """
  Country name
  """
  country: String

  """
  Country code
  """
  countryCode: String

  """
  Region name
  """
  region: String

  """
  Region or state code
  """
  regionCode: String
}


```

TypeGraphQL exposes the `description` attribute to inject comments into the generated schema.


```typescript

@ObjectType({ description: "The recipe model" })
class Recipe {
  @Field(type => ID)
  id: string;

  @Field({ description: "The title of the recipe" })
  title: string;

  @Field(type => [Rate])
  ratings: Rate[];

  @Field({ nullable: true })
  averageRating?: number;
}

```

You could use GraphQL Playground to host a live version of your api docs for GraphQL but it helps to have a static version incase you don't want people hitting the api unless they don't really have an account.

To generate the docs you would need to feed the schema to (Docusaurus)[https://docusaurus.io/docs].If you are using type-graphql to generate static docs is to first emit the GraphQL schema https://typegraphql.com/docs/emit-schema.html#docsNav. 


1. Scaffold a simple docusaurus 
> npx @docusaurus/init@latest init generate-gql-docs classic

2. Install generator
> npm install --save @edno/docusaurus2-graphql-doc-generator

3. Change config in `docusaurus.config.js` to point to the GraphQL Schema

```typescript
    plugins: [
    [
      require.resolve('@edno/docusaurus2-graphql-doc-generator'),
      {
        schema: './schema.gql',
        rootPath: './docs', // docs will be generated under './docs/swapi' (rootPath/baseURL)
        baseURL: 'api',
        linkRoot: '/docs',
      },
    ],
  ],
```

4. Generate docs
> npx docusaurus graphql-to-doc


5. To see it in action
> npm run start

Code for this is here https://github.com/visheshd/generate-gql-docs

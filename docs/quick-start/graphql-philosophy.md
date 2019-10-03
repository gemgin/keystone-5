<!--[meta]
section: quick-start
title: GraphQL Philosophy
order: 1
[meta]-->

# GraphQL Philosophy

## Goals

A good GraphQL API is a combination of the following criteria:

* **Quick prototyping** no matter the client (mobile, desktop, other APIs, etc)
* Be **obvious**, **consistent**, and **predictable**
* Is mostly **CRUD-based** with escape hatches for **Custom Operations**
* Match developer's **domain knowledge**
* Be **forward compatible** with future unknown use-cases
* Fully **leverage the _Graph_** of GraphQL through Relationships

## Keystone's Schema Design

Keystone's auto-generated GraphQL Schema meets these goals by following a pattern with two distinct sets of things:

1. **Domain Objects**

    Modelled with CRUD (_Create, Read, Update, Delete_) operations, this covers the majority of functionality for most applications.
    
    For example; the `User` type would have `createUser` / `getUser` / `updateUser` / `deleteUser` mutations.

1. **Custom Operations**.

    Become apparent over time while building applications and adding to the schema.

    For example; an `authenticateUser` / `submitTPSReport` mutation, or a `recentlyActiveUsers` query.

<p align="center">
  <a href="https://twitter.com/JessTelford/status/1179175687560630272">
    <img src="./img/tweet-graphql-2-things.png" alt="Tweet by Jess Telford: In my experience, the best GraphQL APIs have 2 distinct sets of things: 1. Domain Objects are modelled as type with CRUD mutations (`createUser`/`updateUser`/etc). 2. Common actions involving 0 or more Domain Objects are mutations (`sendEmail`/`finalizeTPSReport`)" width="500" />
  </a>
</p>

<sub align="center">

_[Tweet](https://twitter.com/JessTelford/status/1179175687560630272) by [Jess Telford](https://twitter.com/JessTelford)_

</sub>

<br />

### Domain Objects & CRUD Operations

CRUD Operations enable fast iteration, with a consistent and predictable set of mutations and queries for every Domain Object.

### Custom Operations

Custom Operations are an emergent property of the schema design. They are not something which should be defined up front.

As products are built, it will become obvious which operations are missing and what their inputs/outputs should be.

For example, while building out the TPS application, it became evident that at some point a TPS Report had to be printed and handed directly to a boss. There is no CRUD operation which can trigger printing a report. There are, however, the _Printing_ and _Courier_ services. A custom mutation can be made which uses both those services to complete the operation: `submitTPSReport`.

```javascript
const typeDefs = `
  type Mutation {
    submitTPSReport(TPSReportId: String, bossId: String): Boolean
  }
`;

const resolvers = {
  Mutation: {
    submitTPSReport: async (_, { TPSReportId, bossId }) => {
      await printService.printTPSReport(TPSReportId);
      const address = await getAddress(bossId);
      await courierService.submitJob({ from: 'printer', to: address });
      return true;
    }
  }
};

const server = new ApolloServer({ typeDefs, resolvers });
```

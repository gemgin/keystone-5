<!--[meta]
section: quick-start
title: GraphQL Philosophy
order: 1
[meta]-->

# GraphQL Philosophy

## Goals

A good GraphQL API is a combination of the following criteria:

* Enable quick prototyping no matter the client (mobile, desktop, other APIs, etc)
* Match developer's mental models of the domain
* Be _obvious_, _consistent_, and _predictable_
* Be forward compatible with future unknown use-cases
* Fully leverage the _Graph_ of GraphQL through Relationships
* Is mostly CRUD-based with escape hatches for Custom Operations

## Keystone's Schema Design

Keystone's auto-generated GraphQL Schema meets these goals by following a pattern with two distinct sets of things:

1. **Domain Objects**, modelled with CRUD (_Create, Read, Update, Delete_) operations.
    For example; the `User` type would have `createUser` / `getUser` / `updateUser` / `deleteUser` mutations.

1. **Custom Operations**.
    For example; an `authenticateUser` / `submitTPSReport` mutation, or a `recentlyActiveUsers` query.

<span align="center">

[![Tweet by Jess Telford: In my experience, the best GraphQL APIs have 2 distinct sets of things: 1. Domain Objects are modelled as type with CRUD mutations (`createUser`/`updateUser`/etc). 2. Common actions involving 0 or more Domain Objects are mutations (`sendEmail`/`finalizeTPSReport`)](./img/tweet-graphql-2-things.png)](https://twitter.com/JessTelford/status/1179175687560630272)

  <sub align="center">

_[Tweet](https://twitter.com/JessTelford/status/1179175687560630272) by [Jess Telford](https://twitter.com/JessTelford)_

  </sub>
</span>

<br />

CRUD operations are what enable fast iteration of different clients, with a consistent and predictable set of mutations and queries for every Domain Object. This will cover about 90% of the functionality of any application. The final 10% is then covered with Custom Operations which become apparent over time while building the schema.

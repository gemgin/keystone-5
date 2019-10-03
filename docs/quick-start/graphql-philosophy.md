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

Keystone's auto-generated GraphQL Schema meets these goals by following the pattern:

[![Tweet by Jess Telford: In my experience, the best GraphQL APIs have 2 distinct sets of things: 1. Domain Objects are modelled as type with CRUD mutations (`createUser`/`updateUser`/etc). 2. Common actions involving 0 or more Domain Objects are mutations (`sendEmail`/`finalizeTPSReport`)](./img/tweet-graphql-2-things.png)](https://twitter.com/JessTelford/status/1179175687560630272)


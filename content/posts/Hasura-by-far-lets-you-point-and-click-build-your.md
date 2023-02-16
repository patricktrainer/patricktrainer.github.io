---
date: '2021-01-01'
draft: false
tags: '[]'
title: Hasura-by-far-lets-you-point-and-click-build-your
---

# Hasura-by-far-lets-you-point-and-click-build-your

# Hasura by far, lets you point-and-click build your database and table relationsh... | Hacker News
Created: April 5, 2020 5:02 PM
URL: https://news.ycombinator.com/item?id=22787313
Hasura by far, lets you point-and-click build your database and table relationships with a web dashboard and autogenerates a full GraphQL CRUD API with permissions you can configure and JWT/webhook auth baked-in.
I've been able to build in a weekend no-code what would've taken my team weeks or months to build by hand, even with something as productive as Rails.
It automates the boring stuff and you just have to write single endpoints for custom business logic, like "send a welcome email on sign-up" or "process a payment".
It has a database viewer, but it's not the core of the product, so I use Forest Admin to autogenerate an Admin Dashboard that non-technical team members can use:
With these two, you can point-and-click make 80% of a SaaS product in almost no time.
I wrote a tutorial on how to integrate Hasura + Forest Admin, for anyone interested:
For interacting with Hasura from a client, you can autogenerate fully-typed & documented query components in your framework of choice using GraphQL Code Generator:
Then I usually throw Metabase in there as a self-hosted Business Intelligence platform for non-technical people to use as well, and PostHog for analytics:
All of these all Docker Containers, so you can have them running locally or deployed in minutes.
This stack is absurdly powerful and productive.

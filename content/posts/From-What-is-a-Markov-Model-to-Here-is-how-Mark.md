---
date: '2021-01-01'
draft: false
tags: '[]'
title: From-What-is-a-Markov-Model-to-Here-is-how-Mark
---

# From-What-is-a-Markov-Model-to-Here-is-how-Mark

# From “What is a Markov Model” to “Here is how Markov Models Work” - By
Created: February 21, 2020 12:22 PM
URL: https://hackernoon.com/from-what-is-a-markov-model-to-here-is-how-markov-models-work-1ac5f4629b71
To be honest, if you are just looking to answer the age old question of “what is a Markov Model” you should take a visit to Wikipedia (or just check the TLDR 😉), but if you are curious and looking to use some examples to aid in your understanding of *what* a Markov Model is, *why* Markov Models Matter, and *how to implement* a Markov Model stick around :) **Show > Tell**
> TLDR: “In probability theory, a Markov model is a stochastic model used to model randomly changing systems where it is assumed that future states depend only on the current state not on the events that occurred before it (that is, it assumes the Markov property).
[From%20%E2%80%9CWhat%20is%20a%20Markov%20Model%E2%80%9D%20to%20%E2%80%9CHere%20is%20how%20Mark%20529b583894574a42bfbc7a4658520ee2/1gnwXq22M3L3-bBXibqXqaw.png](From%20%E2%80%9CWhat%20is%20a%20Markov%20Model%E2%80%9D%20to%20%E2%80%9CHere%20is%20how%20Mark%20529b583894574a42bfbc7a4658520ee2/1gnwXq22M3L3-bBXibqXqaw.png)
Distribution of keys
By looking at the above **distribution** of **keys** we could deduce that the **key** fish comes up 4x as much as any other **key.
Lets start from a high level definition of *What* a Markov Model is (according to [Wikipedia](https://en.wikipedia.org/wiki/Markov_model)):
> “A Markov model is a stochastic model used to model randomly changing systems where it is assumed that future states depend only on the current state not on the events that occurred before it (that is, it assumes the Markov property).
Wow, ok so many keys 🔑 were brought up and dictionaries too if you are curious about the code you should certainly check it out below👇 But otherwise, just recognize that in order to create a more advanced model we need to track what **keys** proceed other **keys** and the **amount of occurrences** of these keys.
It has been quite a journey to go from ***what*** is a Markov Model to now be talking about ***how to*** implement a Markov Model 🌄
[From%20%E2%80%9CWhat%20is%20a%20Markov%20Model%E2%80%9D%20to%20%E2%80%9CHere%20is%20how%20Mark%20529b583894574a42bfbc7a4658520ee2/13122645](From%20%E2%80%9CWhat%20is%20a%20Markov%20Model%E2%80%9D%20to%20%E2%80%9CHere%20is%20how%20Mark%20529b583894574a42bfbc7a4658520ee2/13122645)
In my implementation I have a **dictionary** that stores *windows* as the **key in the key-value pair** and then the *value* for each *key* is a **dictogram**.
Nth Order Markov Model Structure |**Some of you are definitely curious about how to **implement higher order Markov Models** so I also included how I went about doing that 😏
☝️☝️☝️☝️☝️ Very similar to the first order Markov Model, but in this case we store a ***tuple*** as the **key** in the **key-value pair** in the **dictionary**.
Otherwise, you start the generated data with a **starting state** (which I generate from valid starts), then you just keep looking at the **possible keys** (by going into the dictogram for that key) that could **follow the current state** and **make a decision** based on *probability* and *randomness* (**weighted probability**).

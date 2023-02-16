---
date: '2023-02-16'
draft: false
title: Consistency-Models
---

# Consistency-Models

# Consistency Models
Created: June 18, 2020 3:07 PM
URL: https://jepsen.io/consistency
This clickable map (adapted from [Bailis, Davidson, Fekete et al](http://www.vldb.org/pvldb/vol7/p181-bailis.pdf) and [Viotti & Vukolic](https://arxiv.org/pdf/1512.00168.pdf)) shows the relationships between common consistency models for concurrent systems.
We say “logically single-threaded” to emphasize that while a process can only do one thing at a time, its implementation may be spread across multiple threads, operating system processes, or even physical nodes—just so long as those components provide the illusion of a coherent singlethreaded program.
To model this, we say that each operation has an *invocation time* and, should it complete, a strictly greater *completion time*, both given by an imaginary[2](https://jepsen.io/consistency), perfectly synchronized, globally accessible clock.
[4](https://jepsen.io/consistency)
Since operations take time, two operations might overlap in time.
If an operation does not complete for some reason (perhaps because it timed out or a critical component crashed) that operation *has no completion time*, and must, in general, be considered concurrent with every operation after its invocation.
Some papers represent this as a set of operations, where each operation includes two numbers, representing their invocation and completion time; concurrent structure is inferred by comparing the time windows between processes.
[↩](https://jepsen.io/consistency)
This magical synchronized clock doesn’t actually need to exist, but some consistency models imply that *if such a clock were to exist*, some operations would happen before others.

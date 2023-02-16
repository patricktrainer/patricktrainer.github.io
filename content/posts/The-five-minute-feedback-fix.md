---
date: '2023-02-16'
draft: false
title: The-five-minute-feedback-fix
---

# The-five-minute-feedback-fix

*
### Overview
The core idea of formal specifications is simple: Create a blueprint of your design, write some properties the blueprint should maintain, and test that you have those properties.
### Decision tables
Decision tables are a way of specifying choices your system can make in a given context.
That’s where the *formal* part of the formal specification comes in: If we don’t have exactly six rows, we immediately know the table is somehow wrong.
For simplicity, we’ll assume I only need to implement just the first two options, “How many participants can share at the same time?” and “Who can share?” Under what cases can I share my screen?
There are four possible inputs in our decision table:
- Can only the host share?
Here, the invariant is
*If "only the host can share” is enabled then someone who **isn’t** the host **cannot** share.
That means there’s no missing rows indicating a missing requirement, and no duplicate rows indicating a requirement contradiction.

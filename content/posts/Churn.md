---
date: '2021-01-01'
draft: false
tags: '[]'
title: Churn
---

# Churn

[Churn%203075f664cd834b5b8e5d6924f4ad1f2f/0j3iK6M7Jt1TCV-NX.png](Churn%203075f664cd834b5b8e5d6924f4ad1f2f/0j3iK6M7Jt1TCV-NX.png)
*If a user has a constant churn probability over time, this implies that customer lifetimes come from an Exponential distribution.
If the churn probability gets lower the longer the customer has been subscribed, you could model that as `c/(t+1)`, where `t` is the timestep (e.g. number of days the customer has been subscribed), and `c` is some constant.
[Churn%203075f664cd834b5b8e5d6924f4ad1f2f/0_ceJxW5UQmjQze15.png](Churn%203075f664cd834b5b8e5d6924f4ad1f2f/0_ceJxW5UQmjQze15.png)
*The Lomax distribution can express churn probabilities that get lower with time.
Keep in mind, in each of the examples below we simulate lifetimes from the same customer lifetime distribution, and this distribution **does not change** over time.
Multiply this by what you make per customer per day, and you have your Customer Lifetime Value.
Keep in mind that the *typical customers* (found by the median) stick around equally long in either company, but it’s the rare long term customers that shift the Lifetime Customer Value massively in favor of the orange company.
](http://fooledbyrandomness.com/DarwinCollege.pdf) So if you have Pareto 80/20 distributed customer lifetimes, **you need 100 billion customers before the sample mean lifetime is accurate.

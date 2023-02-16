---
date: '2021-01-01'
draft: false
tags: '[]'
title: Optimal-stopping-Wikipedia
---

# Optimal-stopping-Wikipedia

A sequence of 'reward' functions which depend on the observed values of the random variables in 1.:
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/c347dcdade06ab59406dacf0d929e03855856ee8](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/c347dcdade06ab59406dacf0d929e03855856ee8)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/4f93e8400461ac4d620680baee52030fa89911db](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/4f93e8400461ac4d620680baee52030fa89911db)
Given those objects, the problem is as follows:
- You are observing the sequence of random variables, and at each step , you can choose to either stop observing or continue
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/add78d8608ad86e54951b8c8bd6c8d8416533d20](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/add78d8608ad86e54951b8c8bd6c8d8416533d20)
- If you stop observing at step , you will receive reward
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/67d30d30b6c2dbe4d6f150d699de040937ecc95f](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/67d30d30b6c2dbe4d6f150d699de040937ecc95f)
- You want to choose a [stopping rule](https://en.wikipedia.org/wiki/Stopping_rule) to maximize your expected reward (or equivalently, minimize your expected loss)
### Continuous time case[[edit](https://en.wikipedia.org/w/index.php?title=Optimal_stopping&action=edit&section=3)]
Consider a gain processes
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/3145251bd7dcd62f06889457914d47d54447646a](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/3145251bd7dcd62f06889457914d47d54447646a)
defined on a [filtered probability space](https://en.wikipedia.org/wiki/Filtered_probability_space)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/5e3f1b6d200f2bc4fd12f17fcd4b9547da96ce09](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/5e3f1b6d200f2bc4fd12f17fcd4b9547da96ce09)
and assume that
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/f5f3c8921a3b352de45446a6789b104458c9f90b](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/f5f3c8921a3b352de45446a6789b104458c9f90b)
is [adapted](https://en.wikipedia.org/wiki/Adapted_process) to the filtration.
The optimal stopping problem is to find the [stopping time](https://en.wikipedia.org/wiki/Stopping_time)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/0b4ac981f3c6efc49fbcb3ecd24f7bf152dad0a7](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/0b4ac981f3c6efc49fbcb3ecd24f7bf152dad0a7)
which maximizes the expected gain
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/c4da65227df8165056ee82f640793d8e4b37908f](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/c4da65227df8165056ee82f640793d8e4b37908f)
where
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/57a433d75842b2d6a28cd5f8ca9cf7dba459084f](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/57a433d75842b2d6a28cd5f8ca9cf7dba459084f)
is called the [value function](https://en.wikipedia.org/wiki/Value_function).
We consider an adapted strong [Markov process](https://en.wikipedia.org/wiki/Markov_process)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/478bcaa73ef8daeb8bd07701b59c6384b689f131](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/478bcaa73ef8daeb8bd07701b59c6384b689f131)
defined on a filtered probability space
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/becca0fa5b0e6527db1e25d78299511b5320edbb](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/becca0fa5b0e6527db1e25d78299511b5320edbb)
where
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/03c8fe9e48980d22020c362b11762a216f8bee58](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/03c8fe9e48980d22020c362b11762a216f8bee58)
denotes the [probability measure](https://en.wikipedia.org/wiki/Probability_measure) where the [stochastic process](https://en.wikipedia.org/wiki/Stochastic_process) starts at
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/87f9e315fd7e2ba406057a97300593c4802b53e4](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/87f9e315fd7e2ba406057a97300593c4802b53e4)
.
## A jump diffusion result[[edit](https://en.wikipedia.org/w/index.php?title=Optimal_stopping&action=edit&section=5)]
Let
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/95734a78eb8407939c3496cbfd92763ced1e41e1](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/95734a78eb8407939c3496cbfd92763ced1e41e1)
be a [Lévy](https://en.wikipedia.org/wiki/L%C3%A9vy_process) diffusion in
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/1bcd8908c9fa46eb979ef7b67d1bb65eb3692cbb](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/1bcd8908c9fa46eb979ef7b67d1bb65eb3692cbb)
given by the [SDE](https://en.wikipedia.org/wiki/Stochastic_differential_equation)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/264bc8d76ca788b3eff6e45fa24b76c3201aba60](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/264bc8d76ca788b3eff6e45fa24b76c3201aba60)
where
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/47136aad860d145f75f3eed3022df827cee94d7a](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/47136aad860d145f75f3eed3022df827cee94d7a)
is an
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/0a07d98bb302f3856cbabc47b2b9016692e3f7bc](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/0a07d98bb302f3856cbabc47b2b9016692e3f7bc)
-dimensional [Brownian motion](https://en.wikipedia.org/wiki/Brownian_motion),
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/b49f9e15c90b97d6d95aaf6bd1a4f520d66c2bb7](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/b49f9e15c90b97d6d95aaf6bd1a4f520d66c2bb7)
is an
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/829091f745070b9eb97a80244129025440a1cfac](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/829091f745070b9eb97a80244129025440a1cfac)
-dimensional compensated [Poisson random measure](https://en.wikipedia.org/wiki/Poisson_random_measure),
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/aae4bec0dfe664f70a1b9cda15fd319fa1e454eb](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/aae4bec0dfe664f70a1b9cda15fd319fa1e454eb)
,
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/165b2ac51764fbee3ed5db71d915b53420333832](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/165b2ac51764fbee3ed5db71d915b53420333832)
, and
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/454e9f9964b0205f0e19d54a5e902038bc1e095f](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/454e9f9964b0205f0e19d54a5e902038bc1e095f)
are given functions such that a unique solution
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/5446d2e710df1848b39d3474304fa84dbdc60a05](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/5446d2e710df1848b39d3474304fa84dbdc60a05)
exists.
The optimal stopping problem is:
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/96e90fc8d59f61857be4ba95aff689714bfc5761](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/96e90fc8d59f61857be4ba95aff689714bfc5761)
It turns out that under some regularity conditions,[[5]](https://en.wikipedia.org/wiki/Optimal_stopping) the following verification theorem holds:
If a function
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/7d9dd8e4893e28a7f6eabb88b72d49efc8ddeb39](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/7d9dd8e4893e28a7f6eabb88b72d49efc8ddeb39)
satisfies
- where the continuation region is ,
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/8a238ecdc084108386647a9f4928c99d54af39a4](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/8a238ecdc084108386647a9f4928c99d54af39a4)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/9b3f5a2a4a0459b28eb40706f67ea48f83d35b78](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/9b3f5a2a4a0459b28eb40706f67ea48f83d35b78)
- on , and
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/3a8073395c6ee55e9f384471412c9d453ced655f](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/3a8073395c6ee55e9f384471412c9d453ced655f)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/2302a18e269dbecc43c57c0c2aced3bfae15278d](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/2302a18e269dbecc43c57c0c2aced3bfae15278d)
- on , where is the [infinitesimal generator](https://en.wikipedia.org/wiki/Infinitesimal_generator_(stochastic_processes)) of
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/b4b891a2ffc1861ecef13412bb7c69dd7e794891](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/b4b891a2ffc1861ecef13412bb7c69dd7e794891)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/bc33a22fb3a9e91084b653ef5e58815ff05aba06](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/bc33a22fb3a9e91084b653ef5e58815ff05aba06)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/280ae03440942ab348c2ca9b8db6b56ffa9618f8](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/280ae03440942ab348c2ca9b8db6b56ffa9618f8)
then
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/812e58cf6049240099f528ebf2c4b403f7a9ebc7](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/812e58cf6049240099f528ebf2c4b403f7a9ebc7)
for all
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/45c9dab32dcebce045fc69264dc531a98b9bc6c9](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/45c9dab32dcebce045fc69264dc531a98b9bc6c9)
.
Moreover, if
- on
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/ab904cee10099523faefb28ada29590acb97c578](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/ab904cee10099523faefb28ada29590acb97c578)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/f34a0c600395e5d4345287e21fb26efd386990e6](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/f34a0c600395e5d4345287e21fb26efd386990e6)
Then
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/76c271acf29d6893d8a17d35018cc7d8d840ac50](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/76c271acf29d6893d8a17d35018cc7d8d840ac50)
for all
and
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/72be0ff341a0ca9b991ed0249f29a229b223903f](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/72be0ff341a0ca9b991ed0249f29a229b223903f)
is an optimal stopping time.
The solution is known to be[[7]](https://en.wikipedia.org/wiki/Optimal_stopping)
- (Perpetual call) where and
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/62363453bd2df75ecda55d5ef3dba9d954f679a5](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/62363453bd2df75ecda55d5ef3dba9d954f679a5)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/0b5c45a5b03cdca86ea8deb1ec6e2c10ed35d099](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/0b5c45a5b03cdca86ea8deb1ec6e2c10ed35d099)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/fe2ccc20c0bf5cf1d671556648d75d76656fca3d](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/fe2ccc20c0bf5cf1d671556648d75d76656fca3d)
- (Perpetual put) where and
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/e77d9317d3a58cf30457e68bf232480b6afc4a4f](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/e77d9317d3a58cf30457e68bf232480b6afc4a4f)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/fb8e5648b16dcd2cd97fdd295d5ea25ee2224d52](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/fb8e5648b16dcd2cd97fdd295d5ea25ee2224d52)
[Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/10134e66db0d440076b296492c842f996f485e14](Optimal%20stopping%20-%20Wikipedia%2036ca95b1506f4eae8314e9de4cd135fa/10134e66db0d440076b296492c842f996f485e14)
On the other hand, when the expiry date is finite, the problem is associated with a 2-dimensional free-boundary problem with no known closed-form solution.

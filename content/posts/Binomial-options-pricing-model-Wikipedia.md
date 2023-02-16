---
date: '2023-02-16'
draft: false
title: Binomial-options-pricing-model-Wikipedia
---

# Binomial-options-pricing-model-Wikipedia

The binomial model was first proposed by [William Sharpe](https://en.wikipedia.org/wiki/William_F._Sharpe) in the 1978 edition of Investments ([ISBN](https://en.wikipedia.org/wiki/International_Standard_Book_Number) [013504605X](https://en.wikipedia.org/wiki/Special:BookSources/013504605X)),[[1]](https://en.wikipedia.org/wiki/Binomial_options_pricing_model) and formalized by [Cox](https://en.wikipedia.org/wiki/John_Carrington_Cox), [Ross](https://en.wikipedia.org/wiki/Stephen_Ross_(economist)) and [Rubinstein](https://en.wikipedia.org/wiki/Mark_Rubinstein) in 1979[[2]](https://en.wikipedia.org/wiki/Binomial_options_pricing_model) and by Rendleman and Bartter in that same year.
[[citation needed](https://en.wikipedia.org/wiki/Wikipedia:Citation_needed)]
For options with several sources of uncertainty (e.g., [real options](https://en.wikipedia.org/wiki/Real_option)) and for options with complicated features (e.g., [Asian options](https://en.wikipedia.org/wiki/Asian_option)), binomial methods are less practical due to several difficulties, and [Monte Carlo option models](https://en.wikipedia.org/wiki/Monte_Carlo_option_model) are commonly used instead.
At each step, it is assumed that the [underlying instrument](https://en.wikipedia.org/wiki/Underlying_instrument) will move up or down by a specific factor (
[Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/c3e6bb763d22c20916ed4f0bb6bd49d7470cffd8](Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/c3e6bb763d22c20916ed4f0bb6bd49d7470cffd8)
or
[Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/e85ff03cbe0c7341af6b982e47e9f90d235c66ab](Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/e85ff03cbe0c7341af6b982e47e9f90d235c66ab)
) per step of the tree (where, by definition,
[Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/9418b55d44983bad84c6530b9368538a9892b9ef](Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/9418b55d44983bad84c6530b9368538a9892b9ef)
and
[Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/5f15d45850d0fb6f9b86b6ff899f71e679e67374](Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/5f15d45850d0fb6f9b86b6ff899f71e679e67374)
).
Option up
Option down
The following formula to compute the [expectation value](https://en.wikipedia.org/wiki/Expectation_value) is applied at each node:
, or
[Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/b75e23dc7ad848aee9b22bb4cef7cb97ae667b83](Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/b75e23dc7ad848aee9b22bb4cef7cb97ae667b83)
[Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/00282af864f696abbe09d86960fe7d10ed44f0f4](Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/00282af864f696abbe09d86960fe7d10ed44f0f4)
where is the option's value for the node at time t,
[Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/6586a79a20630949cb9f3809b10bc9ba637166cb](Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/6586a79a20630949cb9f3809b10bc9ba637166cb)
[Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/b20367c858b407ee650081aad55d73bc9bfb1850](Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/b20367c858b407ee650081aad55d73bc9bfb1850)
is chosen such that the related [binomial distribution](https://en.wikipedia.org/wiki/Binomial_distribution) simulates the [geometric Brownian motion](https://en.wikipedia.org/wiki/Geometric_Brownian_motion) of the underlying stock with parameters **r** and **σ**,
[Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/30baa98e7511726459fb5f5fd0de92a05366b7a5](Binomial%20options%20pricing%20model%20-%20Wikipedia%20464f7993a1864d5ab474168e8056c9b4/30baa98e7511726459fb5f5fd0de92a05366b7a5)
q is the [dividend yield](https://en.wikipedia.org/wiki/Dividend_yield) of the underlying corresponding to the life of the option.
The aside [algorithm](https://en.wikipedia.org/wiki/Algorithm) demonstrates the approach computing the price of an American put option, although is easily generalized for calls and for European and Bermudan options:
## Relationship with Black–Scholes[[edit](https://en.wikipedia.org/w/index.php?title=Binomial_options_pricing_model&action=edit&section=6)]
Similar [assumptions](https://en.wikipedia.org/wiki/Black%E2%80%93Scholes) underpin both the binomial model and the [Black–Scholes model](https://en.wikipedia.org/wiki/Black%E2%80%93Scholes), and the binomial model thus provides a [discrete time](https://en.wikipedia.org/wiki/Discrete_time_and_continuous_time) [approximation](https://en.wikipedia.org/wiki/Approximation) to the continuous process underlying the Black–Scholes model.
[[5]](https://en.wikipedia.org/wiki/Binomial_options_pricing_model) [[4]](https://en.wikipedia.org/wiki/Binomial_options_pricing_model)
In addition, when analyzed as a numerical procedure, the CRR binomial method can be viewed as a [special case](https://en.wikipedia.org/wiki/Special_case) of the [explicit finite difference method](https://en.wikipedia.org/wiki/Finite_difference_method) for the Black–Scholes [PDE](https://en.wikipedia.org/wiki/Partial_differential_equation); see [finite difference methods for option pricing](https://en.wikipedia.org/wiki/Finite_difference_methods_for_option_pricing).
- [Implied binomial tree](https://en.wikipedia.org/wiki/Implied_binomial_tree)
- [Edgeworth binomial tree](https://en.wikipedia.org/wiki/Edgeworth_binomial_tree)
## [[edit](https://en.wikipedia.org/w/index.php?title=Binomial_options_pricing_model&action=edit&section=8)]
## External links[[edit](https://en.wikipedia.org/w/index.php?title=Binomial_options_pricing_model&action=edit&section=9)]
- [The Binomial Model for Pricing Options](http://www.sjsu.edu/faculty/watkins/binomial.htm), Prof. Thayer Watkins
- [Binomial Option Pricing](http://faculty.darden.virginia.edu/conroyb/derivatives/Binomial%20Option%20Pricing%20_f-0943_.pdf) ([PDF](https://en.wikipedia.org/wiki/PDF)), Prof. Robert M. Conroy
- [Binomial Option Pricing Model](http://demonstrations.wolfram.com/BinomialOptionPricingModel/) by Fiona Maclachlan, [The Wolfram Demonstrations Project](https://en.wikipedia.org/wiki/The_Wolfram_Demonstrations_Project)
- [On the Irrelevance of Expected Stock Returns in the Pricing of Options in the Binomial Model: A Pedagogical Note](http://ssrn.com/abstract=844104) by Valeri Zakamouline
- [A Simple Derivation of Risk-Neutral Probability in the Binomial Option Pricing Model](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2428763) by Greg Orosi

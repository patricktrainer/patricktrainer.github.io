---
 	layout: post
 	title: API-Routing-Layers-in-fintech
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# API-Routing-Layers-in-fintechSome examples of this are Alloy (aggregating several identity verification vendors and enabling you to access them from a single API) and Payitoff (aggregating several student loan programs and enabling you to access them all from a single API).
For the fintech building on an routing layer, you might pay a slightly higher per unit price to consume the service (because the routing layer marks up the cost of the underlying vendor) but the overall organizational cost is lower, simply because you don’t have to distort your org by taking on non-core work.
[API%20Routing%20Layers%20in%20fintech%208184cab869324516bfc6424774a9a74d/segment.png](API%20Routing%20Layers%20in%20fintech%208184cab869324516bfc6424774a9a74d/segment.png)
Segment was the first API routing layer I remember seeing.
### One API, multiple vendors
The common thread amongst API routing layers I’ve seens is that they enable a single integration, that allows you to programmatically access multiple vendors without having to do an additional integration.
[API%20Routing%20Layers%20in%20fintech%208184cab869324516bfc6424774a9a74d/alloy.png](API%20Routing%20Layers%20in%20fintech%208184cab869324516bfc6424774a9a74d/alloy.png)
### Advantages for early stage product teams
When done well, an API routing layer gives an early stage product team material advantages.
Advantages:
- Easily switch between KYC vendors
- Reduce costs through switching
- Increasing pass rates by running customers through multiple vendors
- Companies: Alloy
Payroll linking & income verification
- Aggregated Services: ADP, Gusto, Paylocity, Gusto, Trinet, Paychex, Paycor.
Some financial services subdomains with no routing layers include:
Card manufacturing
- Idemia, CPI, G&D, Perfect Plastic, Arroweye
- Advantages: faster card delivery, redundancy
Merchant payment processing
- Stripe, Adyen, Braintree, Worldpay, Globalpayments, Bolt
- Advantages: cost, acceptance, redundancy
Credit checks for loan underwriting
- Vendors: Experian, Transunion, Equifax
- Advantages: cost, coverage
Bank account linking
- Plaid, Yodlee, Quovo, Finicity
- Advantages: Coverage, reliability
Bank account issuing
- Every BAAS platform: Q2, Marqeta, Synapse, Galileo, i2c,
- Advantages: Issuing cost, Reliability
Bank underwriting
- Radius, Evolve, Regions, Sutton
- Advantages: bank account portability
Outside of financial services, there are a few gargantuan domains, such as healthcare, construction, logistics, natural resources, and others that have a high degree of fragmentation and variability between legacy vendors.

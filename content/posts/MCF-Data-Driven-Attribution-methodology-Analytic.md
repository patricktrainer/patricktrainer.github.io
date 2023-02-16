
---
    title: MCF-Data-Driven-Attribution-methodology-Analytic
    date: 2021-01-01    
    draft: true
    tags: []
---
# MCF-Data-Driven-Attribution-methodology-Analytic# MCF Data-Driven Attribution methodology - Analytics Help
Created: February 21, 2020 12:08 PM
URL: https://support.google.com/analytics/answer/3191594?hl=en&ref_topic=3180362
There are two main parts to the Multi-Channel Funnels (MCF) Data-Driven Attribution methodology: (1) analyzing *all* of your available path data to develop custom conversion probability models, and (2) applying to that probabilistic data set a sophisticated algorithm that assigns partial conversion credit to your marketing touchpoints.
## Develop conversion probability models from *all* available path data
MCF Data-Driven Attribution uses all available path data—including data from both converting *and* non-converting users—to understand how the presence of particular marketing touchpoints impacts your users’ probability of conversion.
## Algorithmically assign conversion credit to marketing touchpoints
MCF Data-Driven Attribution then applies to this probabilistic data set an algorithm based on a concept from cooperative game theory called the *Shapley Value*.
In the case of MCF Data-Driven Attribution, the “team” being analyzed has marketing touchpoints (e.g., *Organic Search*, *Display*, and *Email*) as “team members,” and the “output” of the team is conversions.
The MCF Data-Driven Attribution algorithm computes the counterfactual gains of each marketing touchpoint—that is, it compares the conversion probability of similar users who were exposed to these touchpoints, to the probability when one of the touchpoints does not occur in the path.
This means that the MCF Data-Driven Attribution algorithm takes into account the order in which each touchpoint occurs and assigns different credit for different path positions.
[MCF%20Data-Driven%20Attribution%20methodology%20-%20Analytic%202981068ac24846aa90bd6729b788f890/tMncmkROzRFPKDix5qqyoZ2VPUrOdSpS_Z1C5GOiMAFPorZQuGjt5rPv4zrN6-nOoRaFTxNtw520](MCF%20Data-Driven%20Attribution%20methodology%20-%20Analytic%202981068ac24846aa90bd6729b788f890/tMncmkROzRFPKDix5qqyoZ2VPUrOdSpS_Z1C5GOiMAFPorZQuGjt5rPv4zrN6-nOoRaFTxNtw520)
illustration of display increasing likelihood of purchase
## Explore your MCF Data-Driven model and analyze its ROI implications
You can use the MCF *[Model Explorer](https://support.google.com/analytics/answer/3264219)* report to explore the specific weights your *Data-Driven* model sets based on channel and position.

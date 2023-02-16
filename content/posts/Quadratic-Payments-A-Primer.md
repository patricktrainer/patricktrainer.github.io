---
date: '2023-02-16'
draft: false
title: Quadratic-Payments-A-Primer
---

# Quadratic-Payments-A-Primer

# Quadratic Payments: A Primer
Created: December 10, 2019 9:55 AM
Tags: Data, Finance
URL: https://vitalik.ca/general/2019/12/07/quadratic.html
*Special thanks to Karl Floersch and Jinglan Wang for feedback*
If you follow applied mechanism design or decentralized governance at all, you may have recently heard one of a few buzzwords: [quadratic voting](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2003531), [quadratic funding](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3243656) and [quadratic attention purchase](https://kortina.nyc/essays/speech-is-free-distribution-is-not-a-tax-on-the-purchase-of-human-attention-and-political-power/).
These ideas have been gaining popularity rapidly over the last few years, and small-scale tests have already been deployed: the [Taiwanese presidential hackathon](https://presidential-hackathon.taiwan.gov.tw/en/) used quadratic voting to vote on winning projects, Gitcoin Grants [used quadratic funding](https://vitalik.ca/general/2019/10/24/gitcoin.html) to fund public goods in the Ethereum ecosystem, and the Colorado Democratic party [also experimented with](https://www.wired.com/story/colorado-quadratic-voting-experiment) quadratic voting to determine their party platform.
[Quadratic%20Payments%20A%20Primer%209d075cbbe1144314a4f35620d936c95d/Market10.png](Quadratic%20Payments%20A%20Primer%209d075cbbe1144314a4f35620d936c95d/Market10.png)
Now let's look at all three beside each other:
[Untitled](Quadratic%20Payments%20A%20Primer%209d075cbbe1144314a4f35620d936c95d/Untitled%20Database%209177707e749c4de59838dbf271efe716.csv)
Notice that only quadratic voting has this nice property that the amount of influence you purchase is proportional to how much you care; the other two mechanisms either over-privilege concentrated interests or over-privilege diffuse interests.
### Quadratic Voting
*See also the original paper: [https://papers.ssrn.com/sol3/papers.cfm?abstract%5fid=2003531](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2003531)*
Let us begin by exploring the first "flavor" of quadratic payments: quadratic voting.
[Quadratic%20Payments%20A%20Primer%209d075cbbe1144314a4f35620d936c95d/Market7.png](Quadratic%20Payments%20A%20Primer%209d075cbbe1144314a4f35620d936c95d/Market7.png)
Note that in the voting case, we're deciding two options, so different people will favor A over B or B over A; hence, unlike the graphs we saw earlier that start from zero, here voting and preference can both be positive or negative (which option is considered positive and which is negative doesn't matter; the math works out the same way)
As shown above, because the n'th vote has a cost of `n`, the number of votes you make is proportional to how much you value one unit of influence over the decision (the value of the decision multiplied by the probability that one vote will tip the result), and hence proportional to how much you care about A being chosen over B or vice versa.
We interpret the quadratic funding as being *a special case* of quadratic voting, where the contributors to a project are voting for that project and there is one imaginary participant voting against it: the subsidy pool.
Quadratic funding is starting to be explored as a mechanism for funding public goods already; [Gitcoin grants](https://vitalik.ca/general/2019/10/24/gitcoin.html) for funding public goods in the Ethereum ecosystem is currently the biggest example, and the most recent round led to results that, in my own view, did a quite good job of making a fair allocation to support projects that the community deems valuable.

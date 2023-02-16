---
                title: You-re-all-calculating-churn-rates-wrong-The-Sta
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # You-re-all-calculating-churn-rates-wrong-The-Sta

If the churn probability gets lower the longer the customer has been subscribed, you could model that as `c/(t+1)`, where `t` is the timestep (e.g. number of days the customer has been subscribed), and `c` is some constant.In this case, this implies that customer lifetimes comes from a [Lomax distribution](https://en.wikipedia.org/wiki/Lomax_distribution).Keep in mind, in each of the examples below we simulate lifetimes from the same customer lifetime distribution, and this distribution **does not change** over time.Multiply this by what you make per customer per day, and you have your Customer Lifetime Value.The distributions will both have the same *median* customer lifetime, but one has a larger *mean* lifetime than the other.Keep in mind that the *typical customers* (found by the median) stick around equally long in either company, but it’s the rare long term customers that shift the Lifetime Customer Value massively in favor of the orange company.](http://fooledbyrandomness.com/DarwinCollege.pdf) So if you have Pareto 80/20 distributed customer lifetimes, **you need 100 billion customers before the sample mean lifetime is accurate.
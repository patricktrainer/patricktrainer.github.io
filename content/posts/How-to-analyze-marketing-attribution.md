---
                title: How-to-analyze-marketing-attribution
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # How-to-analyze-marketing-attribution

- “Simple”, “out-of-the-box” solutions that are cheap, but only offer insight on a limited slice of data
- Marketers that have completely given up on the problem (“trust your gut”) and are exhausted by vendor promises
Marketers have been told that attribution is a data problem -- “Just get the data and you can have full knowledge of what’s working!” -- when really it’s a data *modeling* problem.This playbook assumes you’re operating within a modern data stack , so you already have the infrastructure that you need in place:
- You’re collecting events data with a tool like Snowplow or Segment (though Segment might get a little pricey)
- You’re extracting data from ad platforms using Stitch or Fivetran
- You’re loading data into a modern, cloud data warehouse like Snowflake, BigQuery, or Redshift
- And you’re using dbt so your analysts can model data in SQL
2.There are four main ways to divvy up this point:
- **First touch**: Attribute the entire conversion to the first touch
- **Last touch:** Attribute the entire conversion to the last touch
- **Forty-twenty-forty:** Attribute 40% (0.4 points) of the attribution to the first touch, 40% to the last touch, and divide the remaining 20% between all touches in between
- **Linear:** Divide the point equally among all touches
There’s no hard and fast answer to which attribution method you should use — chat with your marketing team about what’s most appropriate for your company.Join your two data sources together to do this:
```
select
*
from sessions
left join conversion using (customer_id)
where sessions.started_at <= customer_conversions.converted_at
and sessions.started_at >= dateadd(days, -30, customer_conversions.converted_at)
```
We often limit the sessions that count towards attribution to just the sessions within the 30 days that preceded conversion (often referred to as an “attribution window”).So, rather than answering “how many Facebook sessions led to conversions this week?”, we’re choosing to answer “how many conversions this week were a result of Facebook sessions?”.Now that your marketing team knows which channels are leading to the most conversions, they might then ask: “which channel is leading to the **highest value** conversions?”
### 4.That way, we can join across the two data sets to calculate:
- Cost per acquisition: the number of advertising dollars spent to acquire a customer
- Return on ad spend: attributed revenue / ad spend
```
with ad_spend as (
select * from {{ ref('ad_spend') }}
),
attribution as (
select * from {{ ref('attribution_touches') }}
),
-- aggregate first as this is easier to debug / often leads to fewer fanouts
ad_spend_aggregated as (
select
date_trunc('month', date_day) as date_month,
utm_source,
sum(spend) as total_spend
from ad_spend
group by 1, 2
),
attribution_aggregated as (
select
date_trunc('month', converted_at) as date_month,
utm_source,
sum(linear_points) as attribution_points,
sum(linear_revenue) as attribution_revenue
from attribution
group by 1, 2
),
joined as (
select
*,
1.0 * nullif(total_spend, 0) / attribution_points as cost_per_acquisition,
1.0 * attribution_revenue / nullif(total_spend, 0) as return_on_advertising_spend
from attribution_aggregated
full outer join ad_spend_aggregated
using (date_month, utm_source)
)
select * from joined
order by date_month, utm_source
```
This gives us a view of the data like so:
[Untitled](How%20to%20analyze%20marketing%20attribution%20adc986de2cd54c0aaf5fdaea0bc2a97f/Untitled%20Database%200befe6274ee2481a823bf580fe2d606b.csv)
There’s a few things worth noting in this query:
- We aggregated in a CTE and then joined the two CTEs together — I get nervous whenever a join and an aggregation are happening in the same query (too much risk of fanout!We have one here to ensure that
- Conversions that don’t have associated ad spend appear in our result set
- Ad spend that doesn’t result in conversions still appears in our result set
- Often, the utm attributes on your ad spend data won’t perfectly match the utm parameters on your sessions, so you’ll need to do some upstream data cleaning to get this join to work.
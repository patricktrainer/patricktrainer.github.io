
---
    title: Valuing-User-Subscriptions-Over-Time-with-SQL-Sise
    date: 2021-01-01    
    draft: true
    tags: []
---
# Valuing-User-Subscriptions-Over-Time-with-SQL-Sise**Starting from the raw data**
Our primary table is a subscription table that has the company id, plan id, and the start and end dates of each plan:
This data structure allows us to easily analyze some date slices of our data.
For example, we can look at the number of plans started on a given date:
But it doesn’t allow us to see inside of our start and end ranges, such as how many plans were active on a specific date.
Since we only want a limited series of data, we can perform a check using a nested select to make sure that our dates only cover our periods with a plan.
```
with
dates as (
select
(
getdate()::date - row_number() over(order by true)
)::date as plan_date
from
subscriptions
)
, plan_dates as (
select
plan_date
from
dates
where
plan_date >= (
select
min(plan_start)
from
subscriptions
)
)
```
## **Accounting for null dates**
In our subscriptions table we currently have the dates where they have started and ended.
We can accomplish this by using a coalesce statement to evaluate the plan_end value and inserting the current date in the event that it is null:
```
, cleaned_subs as (
select
company_id
, plan_id
, plan_start
, coalesce(plan_end, getdate()::date) as plan_end
from
subscriptions
)
```
## **Joining on inequalities**
Now that we have our cleaned subscription data in one temp table and our relevant dates in another, we can join them together.
## **Aggregating our data**
Now that our data is joined across date ranges, we can perform the next step in our analysis and aggregate the data!
To get this picture of our data, we can join our aggregated data with our plan data to understand the value within each plan:
```
select
plan_date
, plan_id
, plan
, (active_subs * amount) as mrr
from
aggregated_data
join plans on
aggregated_data.plan_id = plans.id
```
Now we are able to see that our users are in fact moving from our Starter plan to a Pro Plan over time and that the growth in revenue is promising!

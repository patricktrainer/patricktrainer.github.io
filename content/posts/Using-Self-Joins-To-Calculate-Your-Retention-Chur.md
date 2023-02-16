---
date: '2021-01-01'
draft: false
tags: '[]'
title: Using-Self-Joins-To-Calculate-Your-Retention-Chur
---

# Using-Self-Joins-To-Calculate-Your-Retention-Chur

Here’s the query:
```
with monthly_activity as (
select distinct
date_trunc('month', created_at) as month,
user_id
from events
)
select
this_month.month,
count(distinct user_id)
from monthly_activity this_month
join monthly_activity last_month
on this_month.user_id = last_month.user_id
and this_month.month = add_months(last_month.month,1)
group by month
```
Our two join conditions are:
1. this_month.month = add_months(last_month.month,1): This sets up how the join works.
Here’s the query:
```
with monthly_activity as (
select distinct
date_trunc('month', created_at) as month,
user_id
from events
)
select
last_month.month + add_months(last_month.month,1),
count(distinct last_month.user_id)
from monthly_activity last_month
left join monthly_activity this_month
on this_month.user_id = last_month.user_id
and this_month.month = add_months(last_month.month,1)
where this_month.user_id is null
group by 1
```
We’ve changed our query in two ways:
1. left join: This includes every row from last month, not just the ones with users who were active this month.
This leaves us with a table of users who were active last month but not this month, which once again we can group and count over!
Here it is:
```
with first_activity as (
select user_id, date(min(created_at)) as month
from events
group by 1
)
```
We’re going to include all active users each month for whom:
1.
Here’s how we do it:
```
with
monthly_activity as (
select distinct
date_trunc('month', created_at) as month,
user_id
from events
),
first_activity as (
select user_id, date(min(created_at)) as month
from events
group by 1
)
select
this_month.month,
count(distinct user_id)
from monthly_activity this_month
left join monthly_activity last_month
on this_month.user_id = last_month.user_id
and this_month.month = add_months(last_month.month,1)
join first_activity
on this_month.user_id = first_activity.user_id
and first_activity.month != this_month.month
where last_month.user_id is null
group by 1
```
Similar to our Churn query, we employ a couple things in tandem:
1. left join: We want every activity from the current month, even if they weren’t active last month.
We want only users who were active this month and not last month.
Combined together, we get users who were active this month, were not active last month, and are not new: Reactivated users!

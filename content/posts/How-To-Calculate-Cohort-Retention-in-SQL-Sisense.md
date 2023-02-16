---
date: '2023-02-16'
draft: false
title: How-To-Calculate-Cohort-Retention-in-SQL-Sisense
---

# How-To-Calculate-Cohort-Retention-in-SQL-Sisense

## **Calculating basic user retention**
The key to calculating retention is counting users who were active at time #1, then counting how many were active at time #2.
An easy way to do this in SQL is to left join your user activity table to itself like so:
```
select *
from activity
left join activity as future_activity on
activity.user_id = future_activity.user_id
and activity.date = future_activity.date - interval '1 day'
```
Now, for every row of user activity, we have — in that same row — their activity 1 day in the future.
This gives us an ideal table for calculating retention with some simple counts:
```
select
activity.date,
count(distinct activity.user_id) as active_users,
count(distinct future_activity.user_id) as retained_users,
count(distinct future_activity.user_id) /
count(distinct activity.user_id)::float as retention
from activity
left join activity as future_activity on
activity.user_id = future_activity.user_id
and activity.date = future_activity.date - interval '1 day'
group by 1
```
We get this chart:
For extra credit, change the 1-day retention to 7-day or 30-day to capture a sense of longer-term user engagement.
To calculate new user retention, simply join in your users table and only look at activity rows that occurred on the user’s join date:
```
select
users.date as date,
count(distinct activity.user_id) as new_users,
count(distinct future_activity.user_id) as retained_users,
count(distinct future_activity.user_id) /
count(distinct activity.user_id)::float as retention
from activity
-- Limits activity to activity from new users
join users on
activity.user_id = users.id
and users.date = activity.date
left join activity as future_activity on
activity.user_id = future_activity.user_id
and activity.date = future_activity.date - interval '1 day'
group by 1
```
We see that while overall retention is 46%, new user retention is only 5.8%!
Our query now looks like:
```
select
activity.date as date,
count(distinct activity.user_id) as new_users,
count(distinct future_activity.user_id) as retained_users,
count(distinct future_activity.user_id) /
count(distinct activity.user_id)::float as retention
from activity
-- Limits activity to activity from existing users
join users on
activity.user_id = users.id
and users.date != activity.date
left join activity as future_activity on
activity.user_id = future_activity.user_id
and activity.date = future_activity.date - interval '1 day'
group by 1
```
As expected, existing user retention is higher than the overall average: 66% vs. 46%.
* from activity
join users on
users.id = activity.user_id
and users.date = activity.date
)
```
Cohort_active_user_count calculates the total number of active users — the denominator in our retention calculation — in each daily cohort:
```
, cohort_active_user_count as (
select
date, count(distinct user_id) as count
from new_user_activity
group by 1
)
```
On top of that, we’ll make a few smaller changes to the main query:
Calculate the retention period — the number days retained — as future_activity.date – new_user_activity.date and group by it.
Without further ado:
```
select date, 'Day '|| to_char(period, 'DD') as period,
new_users, retained_users, retention
from (
select
new_user_activity.date as date,
(future_activity.date
- new_user_activity.date) as period,
max(cohort_size.count) as new_users, -- all equal in group
count(distinct future_activity.user_id) as retained_users,
count(distinct future_activity.user_id) /
max(cohort_size.count)::float as retention
from new_user_activity
left join activity as future_activity on
new_user_activity.user_id = future_activity.user_id
and new_user_activity.date < future_activity.date
and (new_user_activity.date + interval '10 days')
>= future_activity.date
left join cohort_active_user_count as cohort_size on
new_user_activity.date = cohort_size.date
group by 1, 2) t
where period is not null
order by date, period
```
Notice also the range join, [one of our favorite SQL tricks](https://www.sisense.com/blog/range-joins-give-you-accurate-histories/), to get multiple days of retention in one chart.

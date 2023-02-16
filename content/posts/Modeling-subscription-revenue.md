
---
    title: Modeling-subscription-revenue
    date: 2021-01-01    
    draft: true
    tags: []
---
# Modeling-subscription-revenueThese data points help the business understand the health of your subscriber base, specifically:
- The health of your subscriber base even when you have seasonality in renewals (since you amortize your revenue over months)
- The source of revenue changes: new customers, upgrades, downgrades, churns, or reactivations
- The value of a customer based on how long a given user keeps paying you money: customer lifetime value, average contract value
Frequently, this is called **Monthly Recurring Revenue (MRR) analysis**, with the output looking something like this:
!
As a result, the queries in our dashboard are really simple – here’s one to calculate the number of customers and total MRR for each month:
```
select
date_month,
sum(is_active::integer) as customers,
sum(mrr) as mrr,
from analytics.fct_mrr
group by 1
```
Building the dashboard on top of a data model, rather than raw data, offers a number of benefits:
- **Your business logic is codified**: Every business is unique, and the way your business defines a churn is likely to be subtly different to another business.
[Untitled](Modeling%20subscription%20revenue%2063596882e0ec410dbd78a3337a5e3d3f/Untitled%20Database%2047a46934b024488eb7e787fc807a185e.csv)
The change categories are worth going through here:
- **new**: the customer is a new customer that has not had a previous subscription
- **churn**: last month the customer paid for a subscription, but this month is not.
A customer can churn many times
- **upgrade**: the customer has increased their usage and is now paying you more money per month
- **downgrade**: the customer has decreased their usage and is now paying you less money per month
- **reactivation**: a previously churned customer has started subscribing again
If you're ready to dive straight into a dbt project to see how this is done, check out our sample MRR project [here](https://www.getdbt.com/mrr-playbook/#!/overview).
### Step 2: Date spine subscriptions to have one record per customer per month
*Required SQL technique: [date spining](https://discourse.getdbt.com/t/finding-active-days-for-a-subscription-user-account-date-spining/265) | Required dbt technique: [packages](https://docs.getdbt.com/docs/package-management)*
Since we want to look at the change month-by-month, we need to fan out our subscriptions to have one record per month, rather than one record per active subscription:
[Untitled](Modeling%20subscription%20revenue%2063596882e0ec410dbd78a3337a5e3d3f/Untitled%20Database%20ea5f733c523d45e9bb9abbd7eb94b82e.csv)
Typically, we do this by joining to a table of “months”:
```
select
months.date_month,
subscriptions.customer_id,
subscriptions.subscription_id,
susbcriptions.monthly_revenue
from subscriptions
inner join months
-- all months after start date
on months.date_month >= customers.date_month_start
-- and before end date
and months.date_month <= customers.date_month_end
```
We use the [date_spine](https://github.com/fishtown-analytics/dbt-utils#date_spine-source) macro from the dbt-utils [package](https://docs.getdbt.com/docs/package-management) to generate a table of all months.
```
with customers as (
select
customer_id,
date_trunc('month', min(start_date)) as date_month_start,
date_trunc('month', max(end_date)) as date_month_end
from subscription_periods
group by 1
),
customer_months as (
select
customers.customer_id,
months.date_month
from customers
inner join months
-- all months after start date
on months.date_month >= customers.date_month_start
-- and before end date
and months.date_month < customers.date_month_end
),
-- join the customer_months spine to MRR base model
joined as (
select
customer_months.date_month,
customer_months.customer_id,
coalesce(subscription_periods.monthly_amount, 0) as mrr
from customer_months
left join subscription_periods
on customer_months.customer_id = subscription_periods.customer_id
-- month is after a subscription start date
and customer_months.date_month >= subscription_periods.start_date
-- month is before a subscription end date
and customer_months.date_month < subscription_periods.end_date
)
...
```
### Step 3: Identify the first- and last-active months for a customer
*Required SQL technique: Window functions*
Now that we have all the months for a customer, we can start building some fields to help us categorize the changes.
```
...
final as (
select
date_month,
customer_id,
mrr,
mrr > 0 as is_active,
-- calculate first and last months
min(case when is_active then date_month end) over (
partition by account_id
) as first_active_month,
max(case when is_active then date_month end) over (
partition by account_id
) as last_active_month,
-- calculate if this record is the first or last month
first_active_month = date_month as is_first_month,
last_active_month = date_month as is_last_month
from joined
)
select * from final
```
### Step 4: Generate a “churn” month
Our customer’s last subscription finished in July, so they should get marked as a churn in August.

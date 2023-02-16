
---
    title: Don-t-nest-your-curlies
    date: 2021-01-01    
    draft: true
    tags: []
---
# Don-t-nest-your-curlies# Don't nest your curlies
Created: March 6, 2020 10:01 AM
URL: https://docs.getdbt.com/docs/dont-nest-your-curlies
**Don't Nest Your Curlies**
> If dbt errors out earlyand your models are building quite poorlydon't post to the slackjust take a step backand check if you're nesting your curlies.
>
When writing jinja code in a dbt project, it may be tempting to nest expressions inside of each other.
Take this example:
```
{{ dbt_utils.date_spine(
datepart="day",
start_date=[ USE JINJA HERE ]
)
}}
```
To nest a jinja expression inside of another jinja expression, simply place the desired code (without curly brackets) directly into the expression.
Once we've denoted that we're inside a jinja expression (using the `{{` syntax), no further curly brackets are required inside of the jinja expression.
{{ dbt_utils.date_spine(
datepart="day",
start_date="{{ var('start_date') }}"
)
}}
```
There is one exception to this rule: curlies inside of curlies are acceptable in hooks (ie.
Code like this is both valid, and encouraged:
```
{{ config(post_hook="grant select on {{ this }} to role bi_role") }}
```
So why are curlies inside of curlies allowed in this case?
"table"....` being executed against the database.

---
                title: The-Most-Underutilized-Function-in-SQL
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # The-Most-Underutilized-Function-in-SQL

## #1: Building Yourself a Unique ID
I’m going to make a really strong statement here, but it’s one that I really believe in: **every single [data model](http://dbt.readthedocs.io/en/docs-0.6.0/guide/building-models/) in your warehouse should have a rock solid unique ID**.One reason is that your source data doesn’t have a unique key—if you’re syncing advertising performance data from Facebook Ads via [Stitch](http://stitchdata.com/) or [Fivetran](http://fivetran.com/), the source data in your ad_insights table doesn’t have a unique key you can rely on.Using that knowledge, you can build yourself a unique id using md5():
```
select
md5(date_start::varchar || ad_id::varchar) as insight_id
from
stitch_fb_ads.facebook_ads_insights
limit 5;
insight_id
----------------------------------
6d475ea96f23b097b51ed500116d8c5e 822c9429eabb28ccbcd7286836d7cd60 8b7fcd2aff879772ccac4f0f8bcb6a45 8a2cfd7eb1a723c49db47232e73ca29c 10338719dfadb3d4c9d44c608063998a
(5 rows)
```
The resulting hash is a meaningless string of alphanumeric text that functions as a unique identifier for your record.Of course, you could just as easily just create a single concatenated varchar field that performed the same function, but *it’s actually important to obfuscate the underlying logic behind the hash*: you will innately treat the field differently if it looks like an id versus if it looks like a jumble of human-readable text.We create unique keys for every table and then test uniqueness on this key using [dbt schema tests](http://dbt.readthedocs.io/en/master/guide/testing/).You have the same Facebook Ads dataset as referenced earlier but this time you have a new challenge: join that data to data in your web analytics sessions table so that you can calculate Facebook [ROAS](http://www.verticalrail.com/kb/calculate-roas/).Here’s a code snippet from a client project where we did exactly this:
You can see that this code is actually building the id on top of even more fields: in this example we’re actually unioning together advertising spend data from 7 different ad channels, and the data from Bing and Adwords is identified by ad_group_id and keyword_id instead of by UTM parameters.
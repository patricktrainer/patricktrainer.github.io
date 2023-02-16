---
 	layout: post
 	title: 4-questions-to-help-accurately-scope-analytics-eng
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# 4-questions-to-help-accurately-scope-analytics-engOne common example: your company might have marketing data stored in Marketo, but it is ingested into your data warehouse through an existing Salesforce integration.
The two-hop integration will have more opportunities for failure, and the data will likely not be as granular or complete as the primary source data.
According to [Kimball](https://www.kimballgroup.com/2007/07/keep-to-the-grain-in-dimensional-modeling/), it’s important to “stick to rich, expressive, atomic-level data that’s closely connected to the original source and collection process.” I couldn’t agree more: granular data gives you *options*, aggregated data is limiting.
One of the most common examples of this in practice is the difference between Google Analytics data exported via the API and Google Analytics 360 data loaded automatically into Bigquery.
Ideally, you want to have access to the absolute most granular data available from the source data system.
It’s important to actually learn about the source data systems whose data you’re interacting with.
As you bring each one of these systems into your pipeline and your data model, you’ll need at least one key to join the data in.

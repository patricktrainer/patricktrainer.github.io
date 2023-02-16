---
date: '2021-01-01'
draft: false
tags: '[]'
title: How-we-scrape-300k-prices-per-day-from-Google-Flig
---

# How-we-scrape-300k-prices-per-day-from-Google-Flig

# How we scrape 300k prices per day from Google Flights
Created: June 13, 2020 2:23 PM
URL: https://medium.com/brisk-voyage/how-we-scrape-300k-flight-prices-per-day-from-google-flights-79f5ddbdc4c0
[0*ohKb6_EQ-Ck-aCuG](How%20we%20scrape%20300k%20prices%20per%20day%20from%20Google%20Flig%204770b638435b4ffdb0e65af5a621c0a0/0ohKb6_EQ-Ck-aCuG)
[Brisk Voyage](https://briskvoyage.com/) finds cheap, last-minute weekend trips for our members.
To find flight and hotel prices, we scrape Google Flights and Google Hotels.
To do this, we fetch around 300,000 flight prices from 25,000 Google Flights pages every day.
**The crawler consists of two Lambda functions:**
- The primary Lambda function ingests messages from the SQS queue, crawls Google Flights, and stores the output.
We define this as a pure Lambda function with Chalice, as this function will be separately triggered:
- The second Lambda function triggers multiple instances of the first function.
These libraries are added to the `vendor` directory inside our Chalice project which tells Chalice to install them on each Lambda `crawl` instance:
As the 50 `crawl` functions start up over ~5 seconds, Chrome instances are launched within each function.
This allows the range key to both serve as a unique identifier and support queries such as “give me the cheapest trips to BED that we’ve crawled in the past 30 minutes”:
```
response = crawled_flights_table.query(
KeyConditionExpression=Key("destination").eq(iata_code) & Key("id").gt(earliest_id),
FilterExpression=Attr("cheapest_entry").eq(1),
)
```
## Monitoring and testing
We use [Dashbird](https://app.dashbird.io/) for monitoring the crawler and everything else that’s run under Lambda.

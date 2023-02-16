---
date: '2021-01-01'
draft: false
tags: '[]'
title: DISTINCT-ON-The-confusing-unique-and-useful-featu
---

# DISTINCT-ON-The-confusing-unique-and-useful-featu

**
> The DISTINCT ON clause will only return the first row based on the DISTINCT ON(column) and ORDER BY clause provided in the query.
### Is there any difference between the results of DISTINCT and DISTINCT ON queries?
[DISTINCT%20ON%20The%20confusing,%20unique%20and%20useful%20featu%200254dbd04e6143d5af762bdaf289732b/distinct-on-query-output-yogesh-chauhan-1.jpg](DISTINCT%20ON%20The%20confusing,%20unique%20and%20useful%20featu%200254dbd04e6143d5af762bdaf289732b/distinct-on-query-output-yogesh-chauhan-1.jpg)
DISTINCT ON query:
Output:
!
[DISTINCT%20ON%20The%20confusing,%20unique%20and%20useful%20featu%200254dbd04e6143d5af762bdaf289732b/distinct-on-query-output-yogesh-chauhan-2.jpg](DISTINCT%20ON%20The%20confusing,%20unique%20and%20useful%20featu%200254dbd04e6143d5af762bdaf289732b/distinct-on-query-output-yogesh-chauhan-2.jpg)
!
[DISTINCT%20ON%20The%20confusing,%20unique%20and%20useful%20featu%200254dbd04e6143d5af762bdaf289732b/distinct-on-query-output-yogesh-chauhan-6.jpg](DISTINCT%20ON%20The%20confusing,%20unique%20and%20useful%20featu%200254dbd04e6143d5af762bdaf289732b/distinct-on-query-output-yogesh-chauhan-6.jpg)
So, if we add all the columns to the GROUP BY clause then we will basically get the same results as just simple DISTINCT query.
[DISTINCT%20ON%20The%20confusing,%20unique%20and%20useful%20featu%200254dbd04e6143d5af762bdaf289732b/distinct-on-query-output-yogesh-chauhan-8.jpg](DISTINCT%20ON%20The%20confusing,%20unique%20and%20useful%20featu%200254dbd04e6143d5af762bdaf289732b/distinct-on-query-output-yogesh-chauhan-8.jpg)
So, we need to write down query like this:
SELECT country, COUNT(contact_name), COUNT(company_name) FROM customers GROUP BY country;
Output:
!
[DISTINCT%20ON%20The%20confusing,%20unique%20and%20useful%20featu%200254dbd04e6143d5af762bdaf289732b/distinct-on-query-output-yogesh-chauhan-9.jpg](DISTINCT%20ON%20The%20confusing,%20unique%20and%20useful%20featu%200254dbd04e6143d5af762bdaf289732b/distinct-on-query-output-yogesh-chauhan-9.jpg)
So, as we can see in the screenshot above, we are getting the number of rows using GROUP BY but if we want the first result from all those groups, we need to use DISTINCT ON and that's why I consider it a powerful feature of Postgres.

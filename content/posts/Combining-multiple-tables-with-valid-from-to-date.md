
---
    title: Combining-multiple-tables-with-valid-from-to-date
    date: 2021-01-01    
    draft: true
    tags: []
---
# Combining-multiple-tables-with-valid-from-to-date# Combining multiple tables with valid from/to date ranges into a single dimension | ORAYLIS
Created: February 1, 2020 2:17 PM
URL: https://www.oraylis.de/blog/combining-multiple-tables-with-valid-from-to-date-ranges-into-a-single-dimension
[Data Integration (ETL - ELT)](https://www.oraylis.de/bi-big-data-blog?tags=8) [Data Modelling](https://www.oraylis.de/bi-big-data-blog?tags=9) [Data Warehouse](https://www.oraylis.de/bi-big-data-blog?tags=4) [Microsoft APS](https://www.oraylis.de/bi-big-data-blog?tags=42)
**Dimensional modeling**
Tracking historical changes within a dimension is a common task in data warehousing and well covered by Ralph Kimball’s slowly changing dimension (SCD) methods.
But the valid from/to dates are usually not a good idea for joining fact data to the associated dimensions because this would result in range lookups (ETL) or date range (between) joins (in SQL or ELT).
[Combining%20multiple%20tables%20with%20valid%20from%20to%20date%20%2074c784b6dd2f4768bc7932ad8a5bc58f/2014_11_image_thumb5.png](Combining%20multiple%20tables%20with%20valid%20from%20to%20date%20%2074c784b6dd2f4768bc7932ad8a5bc58f/2014_11_image_thumb5.png)
The tables reflect a very simple human resources model of four tables, a base table Employee and three detail tables, all joined by the EmployeeNo-field.
The following query for example checks if there are overlapping date ranges in the Employee table by using window functions to retrieve the previous and next date boundaries:
1. , lag([ValidTo],1) over (partition by [EmployeeNo] order by [ValidFrom]) PrevValidTo
2. , lead([ValidFrom],1) over (partition by [EmployeeNo] order by [ValidFrom]) NextValidFrom
3. where (PrevValidTo is not null and PrevValidTo>ValidFrom) or (NextValidFrom is not null and NextValidFrom and < in the where condition to a <>, i.e.
Running this check on all the four tables from above shows that the data is consistent (no faulty rows returned from the query above).
At first, as the resulting valid from/to dates need to reflect all date ranges from all of the four tables, I start by collecting all of those dates:
This gives a list of all valid from/to-dates by employee from all of the four tables with duplicates being removed (since I used a union, not a union all).
So, now we can join the four tables with the date range table making sure to include the proper date range in the join condition.
This could even make it a good idea to include valid from/to dates from other associated tables even if no other information from those tables is yet being used in the data warehouse.

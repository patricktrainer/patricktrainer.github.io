---
                title: CTEs-and-Window-Functions-Unleashing-the-Power-of
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # CTEs-and-Window-Functions-Unleashing-the-Power-of

Ultimately you’ll need to read and refer to the PostgreSQL documentation on [Window Functions](http://www.postgresql.org/docs/8.4/static/functions-window.html) and [Window Function Calls](http://www.postgresql.org/docs/8.4/static/sql-expressions.html#SYNTAX-WINDOW-FUNCTIONS), along with the [tutorial](http://www.postgresql.org/docs/8.4/static/tutorial-window.html) when using them in your own queries.Window functions are a special class of analytic functions that are applied to windows of rows.The frame is another logical concept only used by functions that are relative to the frame (like `first_value` / `last_value`)
I think of window functions as falling into two categories:
- Functions that are also available as traditional analytics functions, such as `count`, `sum`, `avg`, etc.For functions that are also available when using `GROUP BY`, the primary advantage of using them with window functions is it becomes possible to do multiple different grouping operations in a single query.### Window Function Examples: Using Multiple Traditional Aggregates
The following query illustrates the use of multiple count functions over different partitions to compute the percent of reservations that a given restaurant accounts for by locality (city).The things to note in this query are:
- Use of `DISTINCT`: Since window functions append columns to each row, without a `DISTINCT` operator, the query will give you back 1 row for every row in the join.I’ve touched on two of the most powerful features for Redshift analytics, window functions and CTEs, but there’s a lot more functionality in Postgres, much of which is also in RedShift.
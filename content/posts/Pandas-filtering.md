
---
    title: Pandas-filtering
    date: 2021-01-01    
    draft: true
    tags: []
---
# Pandas-filtering# Pandas filtering
Created: January 21, 2020 6:43 PM
Tags: Data
URL: https://news.ycombinator.com/item?id=22106575
TileDB[1] offers an embedded SQL experience for python[2].
We use MariaDB built in embedded mode to allow running sql against TileDB Arrays.
This can be combined with pandas.read_sql to load the results directly into a pandas array.
I wrote this implementation for the embedded SQL, so happy to answer any questions on it.
The embedded SQL in its early stages, but should be fully functional for any queries that MariaDB itself supports.
TileDB and the embedded SQL are both open source, TileDB is MIT licensed and the embedded SQL is under GPL.
[1] [https://tiledb.com/](https://tiledb.com/)
[2] [https://docs.tiledb.com/developer/api-usage/embedded-sql](https://docs.tiledb.com/developer/api-usage/embedded-sql)
(disclosure: TileDB, inc. employee)

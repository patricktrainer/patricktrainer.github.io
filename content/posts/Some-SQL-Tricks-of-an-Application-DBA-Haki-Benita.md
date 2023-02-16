---
date: '2021-01-01'
draft: false
tags: '[]'
title: Some-SQL-Tricks-of-an-Application-DBA-Haki-Benita
---

# Some-SQL-Tricks-of-an-Application-DBA-Haki-Benita

To demonstrate, set up a small schema for a store:
```
DROP TABLE IF EXISTS product CASCADE;
CREATE TABLE product (
id serial PRIMARY KEY,
name TEXT NOT NULL,
price INT NOT NULL
);
INSERT INTO product (name, price)
SELECT random()::text, (random() * 1000)::int
FROM generate_series(0, 10000);
DROP TABLE IF EXISTS customer CASCADE;
CREATE TABLE customer (
id serial PRIMARY KEY,
name TEXT NOT NULL
);
INSERT INTO customer (name)
SELECT random()::text
FROM generate_series(0, 100000);
DROP TABLE IF EXISTS sale;
CREATE TABLE sale (
id serial PRIMARY KEY,
created timestamptz NOT NULL,
product_id int NOT NULL,
customer_id int NOT NULL
);
```
The schema defines different types of constraints such as "not null" and unique constraints.
To set a baseline, start by adding foreign keys to the `sale` table, and then load some data into it:
```
db=# ALTER TABLE sale ADD CONSTRAINT sale_product_fk
db-# FOREIGN KEY (product_id) REFERENCES product(id);
ALTER TABLE
Time: 18.413 ms
db=# ALTER TABLE sale ADD CONSTRAINT sale_customer_fk
db-# FOREIGN KEY (customer_id) REFERENCES customer(id);
ALTER TABLE
Time: 5.464 ms
db=# CREATE INDEX sale_created_ix ON sale(created);
CREATE INDEX
Time: 12.605 ms
db=# INSERT INTO SALE (created, product_id, customer_id)
db-# SELECT
db-# now() - interval '1 hour' * random() * 1000,
db-# (random() * 10000)::int + 1,
db-# (random() * 100000)::int + 1
db-# FROM generate_series(1, 1000000);
INSERT 0 1000000
Time: 15410.234 ms (00:15.410)
```
After defining constraints and indexes, loading a million rows to the table took ~15.4s.
Next, try to load the data into the table first, and only then add constraints and indexes:
Loading data into a table without indexes and constraints was much faster, 2.27s compared to 15.4s before.
Let's populate the table with user data, where roughly 90% of the users are activated:
To query for activated and unactivated users, you might be tempted to create an index on the column `activated`:
When you try to query *unactivated users*, the database is using the index:
The database estimated that the filter will result in 102,567 which are roughly 10% of the table.
In PostgreSQL, there is a way to create an index on only a part of the table, using whats called a [partial index](https://www.postgresql.org/docs/current/indexes-partial.html):
Using a `WHERE` clause, we restrict the rows indexed by the index.
But, PostgreSQL provides other types of indexes such as [BRIN](https://www.postgresql.org/docs/current/brin.html):
> BRIN is designed for handling very large tables in which certain columns have some natural correlation with their physical location within the table
>
BRIN stands for Block Range Index.
If the number of adjacent pages is set to 3, the index will divide the table into the following ranges:
For each range, the BRIN index **keeps the minimum and maximum value**:
Using the index above, try to search for the value 5:
- `[1–3]` - Definitely not here
- `[4–6]` - Might be here
- `[7–9]` - Definitely not here
Using the BRIN index we managed to limit our search to blocks 4–6.

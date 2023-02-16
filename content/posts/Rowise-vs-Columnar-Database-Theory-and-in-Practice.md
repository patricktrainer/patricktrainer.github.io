---
                title: Rowise-vs-Columnar-Database-Theory-and-in-Practice
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # Rowise-vs-Columnar-Database-Theory-and-in-Practice

Theory and in Practice
Created: April 20, 2020 10:08 PM
Tags: Database, SQL
URL: https://medium.com/@mangatmodi/rowise-vs-columnar-database-theory-and-in-practice-53f54c8f6505
Columnar database stores are getting increasingly popular lately especially in analytical query systems as data warehouse solutions.Here comes to major difference about row and columnar DBs
> Row oriented database tries to store whole row of the database in the same block but columnar database stores the values of the columns of subsequent in the same block
>
Following is an excellent diagram from Redshift’s documentation[1] to understand the difference.Easy to guess — Row oriented databases perform best for the operations on the whole row and columnar for the operations on the columns.Column Oriented Operations: Update columns, Aggregations, selecting a few columns, and any other operation, stored procedures, etc.Since disk block contributes a lot to the performance it is recommended to have block size which is enough to fit the whole row for row wise DBs and for columnar keep reasonably high block size so that you can operate of more columnar data at one read.Columnar DBs can optimize a lot of space as they keep homogenous data in a single block, so they can apply strategies to compress the data in a block.This is one of the reasons that Columnar DBs are popular as big data DBs because less storage means fewer costs, faster reads (read fewer blocks).
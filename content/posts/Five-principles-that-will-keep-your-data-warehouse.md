---
                title: Five-principles-that-will-keep-your-data-warehouse
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # Five-principles-that-will-keep-your-data-warehouse

In a data warehouse, you have a lot of objects to name — databases, schemas, relations, columns, users, and shared roles.# Use a separate user for each human being and application connecting to your data warehouse
Before we dive into this, it’s worth noting that different data warehouses treat users, groups, and roles in very different ways (for anyone else that wants to fall down this rabbit hole, I wrote my findings up on [Discourse](https://discourse.getdbt.com/t/the-difference-between-users-groups-and-roles-on-each-data-warehouse/429)).# Grant privileges systematically
Data warehouses provide fine-grained privileges —you can grant any combination of the following privileges to a user or a shared role (in fact, these are just a subset of your options!There’s a balance to be found between being too generous with privileges, where you grant `all` privileges to the `public` group, and being too restrictive with privileges, where a super user has to run a series of complex grant statements for every user that wants to run a select statement.We then grant the following privileges to each of the shared roles in our warehouse:
- **loader**: `create-schema`
- **transformer:** `read-schema`, `create-schema`
- **reporter:** `read-schema` (limited to transformed schemas)
I’ve done a very implementation-focused writeup of the exact statements involved in setting up a warehouse in this way over on [Discourse](https://discourse.getdbt.com/t/the-exact-grant-statements-we-use-in-a-dbt-project/430).The implementation of this varies across data warehouses based on how the warehouse handles inheritance:
- **Postgres**: Create a separate role with superuser privileges, and grant the role to individual users as required.- **Redshift**: Create a separate user, `_super` (e.g. `claire_super`) for each user that requires superuser privileges (superuser privileges can only be given to users, not groups).
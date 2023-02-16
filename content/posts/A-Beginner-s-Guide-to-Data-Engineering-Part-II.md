---
 	layout: post
 	title: A-Beginner-s-Guide-to-Data-Engineering-Part-II
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# A-Beginner-s-Guide-to-Data-Engineering-Part-IIFrom collecting raw data and building data warehouses to applying Machine Learning, we saw why data engineering plays a critical role in all of these areas.
First, I will introduce the concept of **Data Modeling**, a design process where one carefully defines table schemas and data relations to capture business metrics and dimensions.
**
## Data Modeling, Normalization, and Star Schema
To give an example of the design decisions involved, we often need to decide the extent to which tables should be **[normalized](https://en.wikipedia.org/wiki/Database_normalization)**.
This design focuses on building normalized tables, specifically fact and dimension tables.
The star schema organized table in a star-like pattern, with a fact table at the center, surrounded by dim tables
## **Fact & Dimension Tables**
To understand how to build denormalized tables from fact tables and dimension tables, we need to discuss their respective roles in more detail:
- **Fact tables** typically contain point-in-time transactional data.
Below is a simple example of how fact tables and dimension tables (both are normalized tables) can be joined together to answer basic analytics question such as how many bookings occurred in the past week in each market.
Shrewd users can also imagine that if additional metrics `m_a, m_b, m_c` and dimensions `dim_x, dim_y, dim_z` are projected in the final `SELECT` clause, a denormalized table can be easily built from these normalized tables.

---
date: '2023-02-16'
draft: false
title: Creating-Data-Vault-Point-In-Time-and-Dimension-ta
---

# Creating-Data-Vault-Point-In-Time-and-Dimension-ta

# Creating Data Vault Point-In-Time and Dimension tables: merging historical data sources - Roelant Vos
Created: February 1, 2020 2:17 PM
URL: http://roelantvos.com/blog/creating-data-vault-point-in-time-and-dimension-tables-merging-historical-data-sources/
**Edit 2019-09-05**: I reviewed this paper on relevance today and made a few minor tweaks.
## Merging time-variant data
Beyond creating Hubs, Links and Satellites and current-state (Type 1) views off a Data Vault model, one of the most common requirements is the ability to represent a complete history of changes for a specific business entity (Hub, Link or groups of those).
This post outlines how merging time-variant data can be applied to Data Vault in order to create Point-In-Time (PIT) and Dimension tables.
To keep some differentiation between the two let’s agree that a PIT table combines history from its direct surrounding tables (all Satellites for a Hub for example).
## Joining historised data sets together
The basic approach to join two time-variant tables together is to join them on their shared key (CUSTOMER_SK in the example below) as well as their Effective and Expiry Date/Times.
## Making joining easier when you have multiple tables in scope
The technique explained in the previous section is geared towards combining *two* time-variant sources and it is not very straightforward (transparent) to add *more* time-variant tables using this approach.
The join uses the same mechanism as above (greatest of the two effective dates < smallest of the two expiry dates) but the big difference is that each time-variant table is joined against the *central* ‘range’ set, making this a lot easier to configure and extend.

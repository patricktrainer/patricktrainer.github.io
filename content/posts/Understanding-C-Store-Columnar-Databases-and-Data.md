---
                title: Understanding-C-Store-Columnar-Databases-and-Data
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # Understanding-C-Store-Columnar-Databases-and-Data

# Understanding C-Store: Columnar Databases and Data Intensive Analytics
Created: April 20, 2020 8:26 AM
URL: https://medium.com/@aakashpydi/understanding-c-store-columnar-databases-and-big-data-analytics-aa669bb60f0
![1*xNYKI1azVyfzhXB-cIvKUw.png](Understanding%20C-Store%20Columnar%20Databases%20and%20Data%20%2098d15be3b76c4c37b71a50b419ddb1f8/1xNYKI1azVyfzhXB-cIvKUw.png)
From what I understand, the first prototype for a columnar database was introduced in a 2005 paper from MIT’s school of computer science and artificial intelligence, called [C-Store: A Column Oriented Database.](http://db.csail.mit.edu/projects/cstore/vldb.pdf)
The key idea from this paper seems to be that, in columnar databases we store each column’s values sequentially in a database, as opposed to storing each row’s values sequentially.- Note that a data block is the smallest unit of data used by a database.- This is a ‘read optimized’ database, particularly in a big data analytics context (which is what we use the large datasets in our columnar database for).The original CSAIL paper notes that write optimized database systems are naturally ideal write heavy applications (such as [Online Transaction Processing](https://docs.microsoft.com/en-us/azure/architecture/data-guide/relational-data/online-transaction-processing) applications) whereas read optimized database systems are naturally ideal for read heavy applications (such as [Data Warehouses](https://aws.amazon.com/data-warehouse/)).My Director, Dan Woicke wrote about the value of using a columnar database to our team’s work here: [Cerner Advances Big Data Analytic Capabilities.
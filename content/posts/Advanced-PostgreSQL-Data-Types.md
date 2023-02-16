---
                title: Advanced-PostgreSQL-Data-Types
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # Advanced-PostgreSQL-Data-Types

The implementation may vary somewhat between systems, but generally there are standard ways you’ll want to process and analyze these types of data (e.g. perform mathematical calculations, find the length of a character string, cast from one type to another, etc).### Array type
Arrays are likely something familiar, but in case you’re new to programming: it’s a data type meant to hold a collection of things.In Postgres, however, the array elements must all be of the same type - the table definition alludes to it:
```
CREATE TABLE countries_visited (
person_name text,
countries char(2)[]
);
```
As we can see above with the countries column, the array declaration must have the type name of the values that array will contain.Another good rule of thumb might be, if there are places in your application code where you’re using arrays and you often find yourself fetching entire data sets, storing the data as an array type could save you one more join against a lookup table.### Range type
You might say that a “range” can describe some set of values, i.e. when something is “within a range,” it is part of that set.Our [second course on data types](https://learn.crunchydata.com/postgresql-devel/courses/basics/advdatatype) in the Crunchy Data interactive learning portal focuses on the above three types plus XML.It lets you play around with these data types with a little sample data, and it also introduces you to some helpful functions and operators that come with these data types.
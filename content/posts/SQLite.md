
---
    title: SQLite
    date: 2021-01-01    
    draft: true
    tags: []
---
# SQLiteTo put it another way, a recursive common table expression must look like the following:
Call the table named by the [cte-table-name](https://www.sqlite.org/syntax/cte-table-name.html) in a recursive common table expression the "recursive table".
A limit of zero means that no rows are ever added to the recursive table, and a negative limit means an unlimited number of rows may be added to the recursive table.
The recursive CTE is then used in the final query:
> WITH RECURSIVE
parent_of(name, parent) AS
(SELECT name, mom FROM family UNION SELECT name, dad FROM family),
ancestor_of_alice(name) AS
(SELECT parent FROM parent_of WHERE name='Alice'
UNION ALL
SELECT parent FROM parent_of JOIN ancestor_of_alice USING(name))
SELECT family.name FROM ancestor_of_alice, family
WHERE ancestor_of_alice.name=family.name
AND died IS NULL
ORDER BY born;
>
A version control system (VCS) will typically store the evolving versions of a project as a directed acyclic graph (DAG).
> WITH RECURSIVE
ancestor(id,mtime) AS (
SELECT id, mtime FROM checkin WHERE id=@BASELINE
UNION
SELECT derivedfrom.xfrom, checkin.mtime
FROM ancestor, derivedfrom, checkin
WHERE ancestor.id=derivedfrom.xto
AND checkin.id=derivedfrom.xfrom
ORDER BY checkin.mtime DESC
LIMIT 20
)
SELECT * FROM checkin JOIN ancestor USING(id);
>
The "ORDER BY checkin.mtime DESC" term in the recursive-select makes the query run much faster by preventing it from following branches that merge checkins from long ago.
To illustrate, we will use a variation on the "org" table from an example above, without the "height" column, and with some real data inserted:
> CREATE TABLE org(
name TEXT PRIMARY KEY,
boss TEXT REFERENCES org
) WITHOUT ROWID;
INSERT INTO org VALUES('Alice',NULL);
INSERT INTO org VALUES('Bob','Alice');
INSERT INTO org VALUES('Cindy','Alice');
INSERT INTO org VALUES('Dave','Bob');
INSERT INTO org VALUES('Emma','Bob');
INSERT INTO org VALUES('Fred','Cindy');
INSERT INTO org VALUES('Gail','Cindy');
>
Here is a query to show the tree structure in a breadth-first pattern:
> WITH RECURSIVE
under_alice(name,level) AS (
VALUES('Alice',0)
UNION ALL
SELECT org.name, under_alice.level+1
FROM org JOIN under_alice ON org.boss=under_alice.name
ORDER BY 2
)
SELECT substr('..........',1,level*3) || name FROM under_alice;
>
The "ORDER BY 2" (which means the same as "ORDER BY under_alice.level+1") causes higher levels in the organization chart (with smaller "level" values) to be processed first, resulting in a breadth-first search.
The output is:
> Alice
...Bob
...Cindy
......Dave
......Emma
......Fred
......Gail
>
But if we change the ORDER BY clause to add the "DESC" modifier, that will cause lower levels in the organization (with larger "level" values) to be processed first by the recursive-select, resulting in a depth-first search:
> WITH RECURSIVE
under_alice(name,level) AS (
VALUES('Alice',0)
UNION ALL
SELECT org.name, under_alice.level+1
FROM org JOIN under_alice ON org.boss=under_alice.name
ORDER BY 2 DESC
)
SELECT substr('..........',1,level*3) || name FROM under_alice;
>
The output of this revised query is:
> Alice
...Bob
......Dave
......Emma
...Cindy
......Fred
......Gail
>
When the ORDER BY clause is omitted from the recursive-select, the queue behaves as a FIFO, which results in a breadth-first search.
Outlandish Recursive Query Examples
The following query computes an approximation of the Mandelbrot Set and outputs the result as ASCII-art:
> WITH RECURSIVE
xaxis(x) AS (VALUES(-2.0) UNION ALL SELECT x+0.05 FROM xaxis WHERE x<1.2),
yaxis(y) AS (VALUES(-1.0) UNION ALL SELECT y+0.1 FROM yaxis WHERE y<1.0),
m(iter, cx, cy, x, y) AS (
SELECT 0, x, y, 0.0, 0.0 FROM xaxis, yaxis
UNION ALL
SELECT iter+1, cx, cy, x*x-y*y + cx, 2.0*x*y + cy FROM m
WHERE (x*x + y*y) < 4.0 AND iter<28
),
m2(iter, cx, cy) AS (
SELECT max(iter), cx, cy FROM m GROUP BY cx, cy
),
a(t) AS (
SELECT group_concat( substr(' .+*#', 1+min(iter/7,4), 1), '')
FROM m2 GROUP BY cy
)
SELECT group_concat(rtrim(t),x'0a') FROM a;
>
In this query, the "xaxis" and "yaxis" CTEs define the grid of points for which the Mandelbrot Set will be approximated.

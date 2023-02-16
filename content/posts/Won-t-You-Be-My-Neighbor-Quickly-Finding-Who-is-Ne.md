---
 	layout: post
 	title: Won-t-You-Be-My-Neighbor-Quickly-Finding-Who-is-Ne
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# Won-t-You-Be-My-Neighbor-Quickly-Finding-Who-is-NeIf we want to find the three friends who were closest to us on October 1, 2012 between 7:00am and 9:00am, we could construct a query like this:
```
SELECT visitor, visited_at, geocode
FROM visits
WHERE
visited_at BETWEEN '2012-10-01 07:00' AND '2012-10-01 09:00'
ORDER BY POINT(40.7127263,-74.0066592) geocode
LIMIT 3;
```
The “K-nearest neighbor” portion of the query can be seen in ORDER BY POINT(40.7127263,-74.0066592) geocode LIMIT 3 which is another of saying “order by the shortest distance between my current location and all the other recorded locations, but find the 3 closest locations to me.”
How does this perform?
Let’s pretend that we still have the [covering indexes](https://info.crunchydata.com/blog/why-covering-indexes-are-incredibly-helpful) in place from the previous article:
```
EXPLAIN ANALYZE SELECT visitor, visited_at, geocode
FROM visits
WHERE
visited_at BETWEEN '2012-10-01 07:00' AND '2012-10-01 09:00'
ORDER BY POINT(40.7127263,-74.0066592) geocode
LIMIT 3;
```
```
Limit (cost=53755.18..53755.54 rows=3 width=48) (actual time=120.890..128.781 rows=3 loops=1)
-> Gather Merge (cost=53755.18..53794.45 rows=328 width=48) (actual time=120.889..128.778 rows=3 loops=1)
Workers Planned: 4
Workers Launched: 4
-> Sort (cost=52755.12..52755.32 rows=82 width=48) (actual time=115.623..115.625 rows=2 loops=5)
Sort Key: (('(40.7127263,-74.0066592)'::point geocode))
Sort Method: top-N heapsort Memory: 25kB
Worker 0: Sort Method: top-N heapsort Memory: 25kB
Worker 1: Sort Method: top-N heapsort Memory: 25kB
Worker 2: Sort Method: top-N heapsort Memory: 25kB
Worker 3: Sort Method: quicksort Memory: 25kB
-> Parallel Seq Scan on visits (cost=0.00..52754.06 rows=82 width=48) (actual time=65.256..115.476 rows=50 loops=5)
Filter: ((visited_at >= '2012-10-01 07:00:00-04'::timestamp with time zone) AND (visited_at <= '2012-10-01 09:00:00-04'::timestamp with time zone))
Rows Removed by Filter: 805600
Planning Time: 0.112 ms
Execution Time: 128.808 ms
```
Looking at this query plan, PostgreSQL determined that none of the indexes could be used, and does a full (parallelized) sequential scan on the visits table in order to find the 3 closest people.
You can use a KNN-GiST index simply by creating a GiST index on a supported data type, which in this case, is the geocode column:
```
CREATE INDEX visits_geocode_gist_idx ON visits USING gist(geocode);
VACUUM ANALYZE visits;
```
To demonstrate its power, let’s see what happens if we try to find the 3 nearest points to a given location:
```
EXPLAIN ANALYZE SELECT visitor, visited_at, geocode
FROM visits
ORDER BY POINT(40.7127263,-74.0066592) geocode
LIMIT 3;
```
```
Limit (cost=0.41..0.73 rows=3 width=48) (actual time=0.237..0.244 rows=3 loops=1)
-> Index Scan using visits_geocode_gist_idx on visits (cost=0.41..423200.97 rows=4028228 width=48) (actual time=0.236..0.242 rows=3 loops=1)
Order By: (geocode '(40.7127263,-74.0066592)'::point)
Planning Time: 0.089 ms
Execution Time: 0.265 ms
```
Wow!
Now let’s try running our original query to find who is closest to us on October 1, 2012 between 7am and 9am and see if this index speeds up:
```
EXPLAIN ANALYZE SELECT visitor, visited_at, geocode
FROM visits
WHERE
visited_at BETWEEN '2012-10-01 07:00' AND '2012-10-01 09:00'
ORDER BY POINT(40.7127263,-74.0066592) geocode
LIMIT 3;
```
```
Limit (cost=0.41..4012.19 rows=3 width=48) (actual time=184.327..184.332 rows=3 loops=1)
-> Index Scan using visits_geocode_gist_idx on visits (cost=0.41..433272.35 rows=324 width=48) (actual time=184.326..184.330 rows=3 loops=1)
Order By: (geocode '(40.7127263,-74.0066592)'::point)
Filter: ((visited_at >= '2012-10-01 07:00:00-04'::timestamp with time zone) AND (visited_at <= '2012-10-01 09:00:00-04'::timestamp with time zone))
Rows Removed by Filter: 499207
Planning Time: 0.140 ms
Execution Time: 184.361 ms
```
No luck: in this case, because we need also need to filter out our data for the given date/time range, PostgreSQL is unable to take advantage of the KNN-GiST index.
You can install this extension by executing the following:
```
CREATE EXTENSION btree_gist;
```
Before we try creating the multicolumn index, first, let’s drop the previous index:
```
DROP INDEX visits_geocode_gist_idx;
```
Now, let’s create the multicolumn index on (visited_at,geocode):
```
CREATE INDEX visits_visited_at_geocode_gist_idx ON visits USING gist(visited_at, geocode);
VACUUM ANALYZE visits;
```
What happens to the execution time?
```
EXPLAIN ANALYZE SELECT visitor, visited_at, geocode
FROM visits
WHERE
visited_at BETWEEN '2012-10-01 07:00' AND '2012-10-01 09:00'
ORDER BY POINT(40.7127263,-74.0066592) geocode
LIMIT 3;
```
```
Limit (cost=0.41..12.64 rows=3 width=48) (actual time=0.047..0.049 rows=3 loops=1)
-> Index Scan using visits_visited_at_geocode_gist_idx on visits (cost=0.41..1348.69 rows=331 width=48) (actual time=0.046..0.048 rows=3 loops=1)
Index Cond: ((visited_at >= '2012-10-01 07:00:00-04'::timestamp with time zone) AND (visited_at <= '2012-10-01 09:00:00-04'::timestamp with time zone))
Order By: (geocode '(40.7127263,-74.0066592)'::point)
Planning Time: 0.133 ms
Execution Time: 0.068 ms
```
Excellent!
They are not without cost: KNN-GiST indexes are larger than regular GiST indexes, but the speedup KNN-GiST indexes provide is significantly (if not orders of magnitude) larger than the additional space and should be in your toolbox for any location-aware application you build.

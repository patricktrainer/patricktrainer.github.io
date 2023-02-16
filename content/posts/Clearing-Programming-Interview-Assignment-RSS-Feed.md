---
date: '2021-01-01'
draft: false
tags: '[]'
title: Clearing-Programming-Interview-Assignment-RSS-Feed
---

# Clearing-Programming-Interview-Assignment-RSS-Feed

Install the necessary libraries for python:
```
docker exec rss-python conda update -c base -c defaults conda
docker exec rss-python conda install beautifulsoup4 lxml psycopg2
docker exec rss-python conda install -c conda-forge apscheduler
```
Let’s start building our data model now…
After reviewing some of the posts, I realised there needs to be three entities:
> 1. posts: Keeping entry of each post published on the feed2.
Please use this ***[github link](https://github.com/vintageplayer/RSS-Parser/blob/master/create_db.sql)*** for the exact create table queries (as they are pretty straightforward)
The tables can be created in one shot by running:
```
docker exec -it rss-postgres psql -U postgres -d audioboom -f create_db.sql
```
**Helper modules**Three scripts apart from the main script were created to abstract some of the underlying functionality with function calls:
> 1. content_fetcher.py: Use to semi-robustly handle a web-page request and return it’s content2.
update_feed_data(***feed***,***conn***):** requests the BeautifulSoup object for the given url and attempts to process any record in it:
```
def update_feed_data(feed,conn):
content = get_soup(feed)
print(f"Processing Records for : {feed}")
records = content.find_all('item')
process_records(records,conn)
return
```
Again, following the functional paradigm, it does its job by retrieving the BeautifulSoup object and passes the content for further processing.
**5. process_records(***content***,** *conn***):** It processes records incrementally and pushes them for persistence (capturing in DB):
```
def process_records(content,conn):
record_count = len(content)
current_max = get_max_records(conn,get_max_query)
print('Current Max : ',current_max)
records = {} if record_count == current_max:
print("No new records found!!")
**6. persist_tastse_of_india_record(***conn***,***data***):** It tries to persist each component of a post separately (based on the entities defined)
```
def persist_taste_of_india_record(conn,data):
persist_record(conn,data,'posts')
persist_record(conn,data['itunes'],'itunes_data')
for media in data['media']:
persist_record(conn,media,'media')
conn.commit()
return True
```
**conn.commit()** is necessary, else the changes in the database aren’t permanent and will be lost once the session expires.
**7. persist_record(***conn***,***data***,***tb_name***):** Execute the insert query based on the object type:
```
def persist_record(conn,data,tb_name):
query_param = tuple(
list(map(lambda k : data[k],col_list[tb_name]))) execute_query(conn,query_strings[tb_name],query_param)
return
```
***query_param*** simply stores the values in the column order in a tuple.
**Executing and scheduling it:** The script is completed by invoking the begin function and scheduling it for once everyday execution as follows:
```
if __name__ == '__main__':
feed_url = 'https://audioboom.com/channels/4930693.rss'
db_credentials = 'connection.json' print('Main Script Running...')
begin(feed_url,db_credentials)
scheduler = BlockingScheduler()
scheduler.add_job(begin, 'interval',[feed_url,db_credentials], hours=24) try:
scheduler.start()
except Exception as e:
print('Stopping Schedule!!')

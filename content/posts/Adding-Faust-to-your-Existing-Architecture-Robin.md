
---
    title: Adding-Faust-to-your-Existing-Architecture-Robin
    date: 2021-01-01    
    draft: true
    tags: []
---
# Adding-Faust-to-your-Existing-Architecture-Robin# Adding Faust to your Existing Architecture - Robinhood Engineering
Created: June 12, 2020 10:58 PM
URL: https://robinhood.engineering/adding-faust-to-your-existing-architecture-39b0ebd1f7c9
A few weeks ago we [open sourced](https://robinhood.engineering/faust-stream-processing-for-python-a66d3a51212d) [Faust](https://github.com/robinhood/faust), a Python stream processing library that we built at [Robinhood](https://robinhood.com/) to make it extremely easy to build and deploy traditionally complex streaming architectures.
We can install [aredis](https://github.com/NoneGG/aredis) and Faust using pip:
```
pip install aredis
pip install faust
```
Upon installing the dependencies, let’s first define our Faust application, Kafka topic and models:
```
import datetime
import faustclass Activity(faust.Record, isodates=True):
user: str
message: str
timestamp: datetime.datetimeapp = faust.App("redis_example", broker="kafka://localhost:9092")
activities_topic = app.topic("feed_activities", value_type=Activity)
```
We can now create an [agent](http://faust.readthedocs.io/en/latest/userguide/agents.html) which reads feed activities coming in through this topic, and adds the messages to the user’s Redis sorted set as follows:
```
@app.agent(activities_topic)
async def save_activities(activities):
async for activity in activities:
client = aredis.StrictRedis(host="localhost", port=6379)
await client.zadd(activity.user, activity.timestamp, activity.message)
```
As shown above, we use Redis as you would use it in any app.
Below is an example of how we use the Python [aiohttp](https://aiohttp.readthedocs.io/en/stable/index.html) library from a Faust streaming app for one of our use cases at Robinhood.
We create an agent which processes orders and uses a third part HTTP API to send order confirmation emails to our customers:
```
async def send_confirmation(order):
url = f"https://emailer.robinhood.com/"
data = {
"user": order.user_id,
"subject": "Order Confirmation",
"body" f"Order: {order.quantity} shares of {order.symbol}",
}
async with aiohttp.ClientSession() as session:
await session.post(url, json=data)@app.agent(orders_topic)
async def add_symbol(orders):
async for order in orders:
await send_confirmation(order)
```
A lot of our internal services export REST APIs.
Again, as before, let us install the Python library we will use to query InfluxDB:
```
pip install aioinflux
```
We now create an agent which looks at the orders topic from above and looks at the time series in InfluxDB for the particular stock to get the price at which the order executed was the price in the market at the time.
```
@app.agent(orders_topic)
async def add_symbol(orders):
async for order in orders:
client = aioinflux.InfluxDBClient()
query = f"SELECT price FROM marketdata WHERE symbol = {order.symbol} AND timestamp <= {order.timestamp} ORDER BY DESC LIMIT 1"
order.market_price = await client.query(query)
await quality_topic.send(key=order.id, value=order)
```
The ability to easily integrate streaming apps with InfluxDB lets us solve problems where we need to work with multiple time series.
```
async def get_top_result(query_string):
client = elasticsearch_async.AsyncElasticsearch()
query = {"query": query_string}
resp = await client.search(index="search_index", body=query)
return resp["hits"]["hits"]@app.agent(search_queries_topic)
async def add_top_search_result(search_queries):
async for query in search_queries:
query.top_result = await get_top_result(query.query_string)
await top_results_topic.send(key=query.top_result, value=query)
```
Faust makes it easy for us to build architectures where we use Elasticsearch as our data store of choice.

---
date: '2021-01-01'
draft: false
tags: '[]'
title: Effortless-API-Request-Caching-with-Python-Redis
---

# Effortless-API-Request-Caching-with-Python-Redis

# Effortless API Request Caching with Python & Redis | Red’s Digressions
Created: May 25, 2020 3:09 PM
URL: https://rednafi.github.io/digressions/python/database/2020/05/25/python-redis-cache.html
Recently, I was working with [MapBox](https://www.mapbox.com/)’s [Route Optimization API](https://docs.mapbox.com/api/navigation/#optimization).
Here the requested coordinate-string will be the key and the response will be the corresponding value
- Setting a timeout on the records
- Serving new requests from cache if the records exist
- Only send a new request to MapBox API if the response is not cached and then add that response to cache
## Setting Up Redis & RedisInsight
To proceed with the above workflow, you’ll need to install and setup Redis database on your system.
```
# docker-compose.yml
version: "3.2"
services:
redis:
container_name: redis-cont
image: "redis:alpine"
command: redis-server --requirepass ubuntu
environment:
- REDIS_PASSWORD=ubuntu
- REDIS_REPLICATION_MODE=master
ports:
- "6379:6379"
volumes:
# save redisearch data to your current working directory
- ./redis-data:/data
command:
# Save if 100 keys are added in every 10 seconds
- "--save 10 100"
# Set password
- "--requirepass ubuntu"
redisinsight: # redis db visualization dashboard
container_name: redisinsight-cont
image: redislabs/redisinsight
ports:
- 8001:8001
volumes:
- redisinsight:/db
volumes:
redis-data:
redisinsight:
```
The above `docker-compose` file has two services, `redis` and `redisinsight`.
```
def route_optima(coordinates: str) -> dict:
# First it looks for the data in redis cache
data = get_routes_from_cache(key=coordinates)
# If cache is found then serves the data from cache
if data is not None:
data = json.loads(data)
data["cache"] = True
return data
else:
# If cache is not found then sends request to the MapBox API
data = get_routes_from_api(coordinates)
# This block sets saves the respose to redis and serves it directly
if data["code"] == "Ok":
data["cache"] = False
data = json.dumps(data)
state = set_routes_to_cache(key=coordinates, value=data)
if state is True:
return json.loads(data)
return data
```
This part of the code wraps the original Route Optimization API and exposes that as a new endpoint.
# coordinates = "90.3866,23.7182;90.3742,23.7461"
return route_optima(coordinates)
```
```
# app.py
import json
import sys
from datetime import timedelta
import httpx
import redis
from fastapi import FastAPI
def redis_connect() -> redis.client.Redis:
try:
client = redis.Redis(
host="localhost",
port=6379,
password="ubuntu",
db=0,
socket_timeout=5,
)
ping = client.ping()
if ping is True:
return client
except redis.AuthenticationError:
print("AuthenticationError")
sys.exit(1)
client = redis_connect()
def get_routes_from_api(coordinates: str) -> dict:
"""Data from mapbox api."""
state = client.setex(key, timedelta(seconds=3600), value=value,)
return state
def route_optima(coordinates: str) -> dict:
# First it looks for the data in redis cache
data = get_routes_from_cache(key=coordinates)
# If cache is found then serves the data from cache
if data is not None:
data = json.loads(data)
data["cache"] = True
return data
else:
# If cache is not found then sends request to the MapBox API
data = get_routes_from_api(coordinates)
# This block sets saves the respose to redis and serves it directly
if data["code"] == "Ok":
data["cache"] = False
data = json.dumps(data)
state = set_routes_to_cache(key=coordinates, value=data)
if state is True:
return json.loads(data)
return data
app = FastAPI()
@app.get("/route-optima/{coordinates}")
def view(coordinates: str) -> dict:
"""This will wrap our original route optimization API and
incorporate Redis Caching.
# coordinates = "90.3866,23.7182;90.3742,23.7461"
return route_optima(coordinates)
```
You can copy the complete code to a file named `app.py` and run the app using the command below (assuming redis, redisinsight is running and you’ve installed the dependencies beforehand):
```
uvicorn app.app:app --host 0.0.0.0 --port 5000 --reload
```
This will run a local server where you can send new request with coordinates.

---
date: '2023-02-16'
draft: false
title: Data-Science-in-Production
---

# Data-Science-in-Production

Instead of doing that, we'll have a server running that's providing the *service* of listening to incoming requests (with model input data) and responding with the model's output, which could be passed on to whatever the next step is (emailing to business stakeholder, passing it into another application, or maybe writing it to a database for further consumption down the line).
We'll create an `app.py` file in our directory so that we end up with this directory structure:
├── housing_app
│ ├── app.py
│ └── .venv
In that file, we can copy/paste the following
```
from flask import Flask
app = Flask(__name__)
@app.route('/')
def hello_world():
return 'Hello, World!'
### Flask Basics
Getting back to business, let's re-examine our `app.py`:
```
# app.py
from flask import Flask
app = Flask(__name__)
@app.route('/')
def hello_world():
return 'Hello, World!'
Here's what that could look like:
```
#app.py
from flask import Flask, request
import pandas as pd
import pickle
app = Flask(__name__)
@app.route('/predict', methods=['POST'])
def predict():
if request.method == 'POST':
# turn json format into pandas dataframe
df = pd.DataFrame.from_records(request.json)
# make predictions and create a df out of them
pred = house_price_model.predict(df[['age']]))
pred = pd.DataFrame(pred, columns=['predicted_price'])
# combine with original data to return it all together
pred = pd.concat([df, pred], axis=1)
return(str(pred))
@app.before_first_request
def load_model():
global house_price_model
with open('house_price_model', 'rb') as handle:
house_price_model = (pickle.load(handle))
```
We've made several changes to our `app.py` that we need to look at.
We've done this because each directory within the `~/housing_app` directory now represents a Docker container - we'll have a `web` container that contains our Flask web application, and we have a new `nginx` container that is going to contain an [nginx](http://web.archive.org/web/20190308184428/https://www.nginx.com/) instance.
There's a lot we can do here, but for now we've left it pretty simple, with a few key commands:
- **build**: this tells Docker which directory to build the container from
- **expose**: this makes port 8000 available to other containers - this is key if containers need to interact with each other
- **command**: this is the final command that is run after the container is created - for out web container we need to create the container, but then also need the Flask application to run, using gunicorn
- **ports**: unlike **expose** this is making port 80 (for HTTP) available to us as the users, rather than available to other containers
- **links**: this creates a link between containers so that we can refer to 'web' simply as 'web' and not worry about the actual IP address
### Deployment
We're finally here!
```
docker-machine create -d virtualbox housing-app-vm
```
Once it's done you can check that your new VM exists by doing:
```
docker-machine ls
```
Now that it's created we just need to make it our current active VM by executing:
```
eval "$(docker-machine env housing-app-vm)"
```
With our `housing_app_vm` VM created and running, we'll execute the following from `~/housing_app` (the location of docker-compose.yml):
```
docker-compose build
docker-compose up -d
```
We'll see a lot of magic happening in the terminal, but when it's done, our containers will be running on our VM and we'll be able to interact with them.

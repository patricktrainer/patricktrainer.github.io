---
date: '2021-01-01'
draft: false
tags: '[]'
title: Collecting-data-from-a-leaflet-map-with-flask-St
---

# Collecting-data-from-a-leaflet-map-with-flask-St

# Collecting data from a leaflet map with flask - Stack Overflow
Created: February 27, 2020 2:27 PM
URL: https://stackoverflow.com/questions/52172010/collecting-data-from-a-leaflet-map-with-flask
!
[apple-touch-icon@2.png](Collecting%20data%20from%20a%20leaflet%20map%20with%20flask%20-%20St%20e9cb5ecdccdb4285b34f8c2c98711b48/apple-touch-icon2.png)
I'm trying to create a webpage with flask.
The webpage includes a leaflet map where I can click on the map to create a marker which opens a popup window with a link.
The link is supposed to open a new page where I can see the longitude and latitude.
I'm currently struggeling on how to send the leaflet coordinates from my js to flask and then to the second route.
Can someone explain to me what I'm doing wrong?
Python file:
```
from flask import Flask, render_template, url_for, request, redirect
app = Flask(__name__)
@app.route('/', methods=["GET","POST"])
def mainpage():
if request.method == "POST":
longitude = request.form["longitude"]
latitude = request.form["latitude"]
return lredirect(url_for("form", longitude=longitude, latitude=latitude))
return render_template("main.html")
@app.route('/form')
def form():
return render_template("form.html")
if __name__ == "__main__":
app.run(debug=True)
```
main.html file:
```

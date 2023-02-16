
---
    title: Quick-Start-Guide-Leaflet-a-JavaScript-library
    date: 2021-01-01    
    draft: true
    tags: []
---
# Quick-Start-Guide-Leaflet-a-JavaScript-library# Quick Start Guide - Leaflet - a JavaScript library for interactive maps
Created: February 15, 2020 8:22 AM
URL: https://leafletjs.com/examples/quick-start/
This step-by-step guide will quickly get you started on Leaflet basics, including setting up a Leaflet map, working with markers, polylines and popups, and dealing with events.
[Untitled](Quick%20Start%20Guide%20-%20Leaflet%20-%20a%20JavaScript%20library%2034abae4121e74559802c946664107c5f/Untitled%20Database%20fa332699d13d4c6cb09f68b5e8a9e01b.csv)
### Preparing your page
Before writing any code for the map, you need to do the following preparation steps on your page:
-
Include Leaflet CSS file in the head section of your document:
```
```
-
Include Leaflet JavaScript file **after** Leaflet’s CSS:
```
```
-
Put a `div` element with a certain `id` where you want your map to be:
```
First we’ll initialize the map and set its view to our chosen geographical coordinates and a zoom level:
```
var mymap = L.map('mapid').setView([51.505, -0.09], 13);
```
By default (as we didn’t pass any options when creating the map instance), all mouse and touch interactions on the map are enabled, and it has zoom and attribution controls.
In this example we’ll use the `mapbox/streets-v11` tiles from [Mapbox’s Static Tiles API](https://docs.mapbox.com/api/maps/#static-tiles) (in order to use tiles from Mapbox, you must also [request an access token](https://www.mapbox.com/studio/account/tokens/)).
### Markers, circles and polygons
Besides tile layers, you can easily add other things to your map, including markers, polylines, polygons, circles, and popups.
Let’s add a marker:
```
var marker = L.marker([51.5, -0.09]).addTo(mymap);
```
Adding a circle is the same (except for specifying the radius in meters as a second argument), but lets you control how it looks by passing options as the last argument when creating the object:
```
var circle = L.circle([51.508, -0.11], {
color: 'red',
fillColor: '#f03',
fillOpacity: 0.5,
radius: 500
}).addTo(mymap);
```
Adding a polygon is as easy:
```
var polygon = L.polygon([
[51.509, -0.08],
[51.503, -0.06],
[51.51, -0.047]
]).addTo(mymap);
```
### Working with popups
Popups are usually used when you want to attach some information to a particular object on a map.
### Dealing with events
Every time something happens in Leaflet, e.g. user clicks on a marker or map zoom changes, the corresponding object sends an event which you can subscribe to with a function.

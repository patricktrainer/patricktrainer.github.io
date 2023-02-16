---
                title: Leaflet-How-to-save-various-marker-position-in-db
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # Leaflet-How-to-save-various-marker-position-in-db

# Leaflet: How to save various marker position in db and load later - Stack Overflow
Created: February 27, 2020 2:03 PM
URL: https://stackoverflow.com/questions/36185565/leaflet-how-to-save-various-marker-position-in-db-and-load-later
![apple-touch-icon@2.png](Leaflet%20How%20to%20save%20various%20marker%20position%20in%20db%20%2096ea249d885b4f31b294b059c333cfe7/apple-touch-icon2.png)
I would do something like this:
```
var map = L.map('mapcanvas').setView([51.505, -0.09], 13);
map.on('click', function(e){
// Place marker
var marker = new L.marker(e.latlng).addTo(map);
// Ajax query to save the values:
var data = {
lat: e.latlng.lat,
lng: e.latlng.lng
}
var request = new XMLHttpRequest();
request.open('POST', '/my/url', true);
request.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded; charset=UTF-8');
request.send(data);
});
```
Although it is probably better to use jQuery.You would then obtain your saved values from the database, store them in a js object, like
```
var positions = [
{
lat: 123.45
lng: 123.45
},
{
lat: 123.45
lng: 123.45
}
]
```
Iterate over them and add markers:
```
for (var i in positions) {
new L.marker([positions[i].lat, positions[i].lng]).addTo(map);
}
```
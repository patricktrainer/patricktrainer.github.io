---
date: '2023-02-16'
draft: false
title: flask-jsondash-schemas-md-at-master-christabor-f
---

# flask-jsondash-schemas-md-at-master-christabor-f

### Examples
- [Dashboard configuration](https://github.com/christabor/flask_jsondash/blob/master/example_app/examples/config/vegalite-fixed.json)
- [Individual dashboard charts data](https://github.com/christabor/flask_jsondash/blob/master/example_app/examples/vegalite)
### Overrides
Supported.
```
{
"data d": 16,
"data e": 77,
"data b": 87,
"data c": 41,
"data a": 15
}
```
### Area
An object with each key corresponding to the line label, and a list of integer values.
### Examples
- [Dashboard configuration](https://github.com/christabor/flask_jsondash/blob/master/example_app/examples/config/plotly.json)
- [Individual dashboard charts data](https://github.com/christabor/flask_jsondash/blob/master/example_app/examples/plotly)
### Overrides
Supported.
### Number Group
Just like the single number option above, a number group has the same options (`color` and `noformat`), and general format, but supports multiple columns for each number (so you can build multiple big display of aggregate values in a single chart):
```
[
{
"title": "Number of widgets sold in last day",
"description": "This is a good sign",
"data": 32515.0,
"color": "green",
},
{
"title": "New customers signed up this week",
"description": "New user accounts created",
"data": 740,
},
{
"title": "Average Daily Users",
"description": "(aka DAU)",
"data": 541200,
},
{
"title": "Max concurrent users this week",
"description": "Server load peak",
"data": 123401,
"color": "orange",
"noformat": true,
},
]
```
You can also override the column width for each item, via `"width": "30%"`.
### Examples
- [Dashboard configuration](https://github.com/christabor/flask_jsondash/blob/master/example_app/examples/config/cytoscape.json)
- [Individual dashboard charts data](https://github.com/christabor/flask_jsondash/blob/master/example_app/examples/cytoscape)
### Overrides
Supported.
### Examples
- [Dashboard configuration](https://github.com/christabor/flask_jsondash/blob/master/example_app/examples/config/sigma.json)
- [Individual dashboard charts data](https://github.com/christabor/flask_jsondash/blob/master/example_app/examples/sigma)
### Overrides
Supported.
Format should be similar to d3 hierarchical layouts, like:
```
{
"children": [
{
"name": "...",
"value": 10
},
{
"name": "...",
"value": 30,
"children": [...]
}
]
}
```
### Examples
- [Dashboard configuration](https://github.com/christabor/flask_jsondash/blob/master/example_app/examples/config/flamegraph.json)
- [Individual dashboard charts data](https://github.com/christabor/flask_jsondash/blob/master/example_app/examples/flamegraph)
## Sparklines
Sparklines are "mini" charts that can be used inline.

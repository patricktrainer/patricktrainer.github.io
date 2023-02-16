---
 	layout: post
 	title: And-voila-Jupyter-Blog
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# And-voila-Jupyter-BlogThe execution model of voilà is the following: upon connection to a notebook URL, voilà launches the kernel for that notebook, and runs all the cells as it populates the notebook model with the outputs.
Voilà can render custom Jupyter widget libraries, including (but not limited to) [bqplot](https://github.com/bloomberg/bqplot), [ipyleafet](https://github.com/jupyter-widgets/ipyleaflet), [ipyvolume](https://github.com/maartenbreddels/ipyvolume), [ipympl](https://github.com/matplotlib/jupyter-matplotlib/), [ipysheet](https://github.com/QuantStack/ipysheet), [plotly](https://github.com/plotly/plotly.py), [ipywebrtc](https://github.com/maartenbreddels/ipywebrtc), etc.
Together with [ipympl](https://github.com/matplotlib/jupyter-matplotlib/), voilà is actually a simple means to render interactive matplotlib figures in a standalone web application:
Voilà can be used to produce applications with any Jupyter kernel.
A voilà template is actually a ***folder*** placed in the standard directory`PREFIX/share/jupyter/voila/templates` and which may include
- `nbconvert` templates (the jinja templates used to transform the notebook into HTML)
- `static` resources
- custom `tornado` templates such as `404.html` etc.
The directory structure for a voilà template is the following:
```
PREFIX/share/jupyter/voila/templates/template_name/|├── conf.json # Template configuration file├── nbconvert_templates/ # Custom nbconvert templates├── static/ # Static directory└── templates/ # Custom tornado templates
```
The voilà template system can be used to completely override the behavior of the front-end.
*
Beyond the `voila` command-line utility, the voilà package also include a Jupyter ***server extension***, so that voilà dashboards can be served alongside the Jupyter notebook application.
Current work streams include better ***integration with JupyterHub*** for publicly sharing dashboard between users, as well as ***JupyterLab extensions*** (a [voilà "preview" extension for notebooks](https://github.com/QuantStack/voila/pull/217), and a WYSIWYG editor for dashboard layouts).

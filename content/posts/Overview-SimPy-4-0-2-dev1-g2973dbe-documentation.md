---
date: '2021-01-01'
draft: false
tags: '[]'
title: Overview-SimPy-4-0-2-dev1-g2973dbe-documentation
---

# Overview-SimPy-4-0-2-dev1-g2973dbe-documentation

# Overview — SimPy 4.0.2.dev1+g2973dbe documentation
Created: June 19, 2020 11:21 AM
URL: https://simpy.readthedocs.io/en/latest/
learn the basics of SimPy in just a couple of minutes for a complete overview
SimPy is a process-based discrete-event simulation framework based on standard Python.
SimPy also provides various types of [shared resources](https://simpy.readthedocs.io/en/latest/topical_guides/resources.html) to model limited capacity congestion points (like servers, checkout counters and tunnels).
Simulations can be performed [“as fast as possible”](https://simpy.readthedocs.io/en/latest/topical_guides/environments.html), in [real time](https://simpy.readthedocs.io/en/latest/topical_guides/real-time-simulations.html) (wall clock time) or by manually [stepping](https://simpy.readthedocs.io/en/latest/topical_guides/environments.html) through the events.
A short example simulating two clocks ticking in different time intervals looks like this:
```
>>> import simpy
>>>
>>> def clock(env, name, tick):
... while True:
... print(name, env.now)
... yield env.timeout(tick)
...
>>> env = simpy.Environment()
>>> env.process(clock(env, 'fast', 0.5))
>>> env.process(clock(env, 'slow', 1))
>>> env.run(until=2)
fast 0
slow 0
fast 0.5
slow 1
fast 1.0
fast 1.5
```
The documentation contains a [tutorial](https://simpy.readthedocs.io/en/latest/simpy_intro/index.html), [several guides](https://simpy.readthedocs.io/en/latest/topical_guides/index.html) explaining key concepts, a number of [examples](https://simpy.readthedocs.io/en/latest/examples/index.html) and the [API reference](https://simpy.readthedocs.io/en/latest/api_reference/index.html).
Simulation model developers are encouraged to share their SimPy modeling techniques with the SimPy community.
Please post a message to the [SimPy mailing list](https://groups.google.com/forum/#!forum/python-simpy).
There is an introductory talk that explains SimPy’s concepts and provides some examples: [watch the video](https://www.youtube.com/watch?v=Bk91DoAEcjY) or [get the slides](http://stefan.sofa-rockers.org/downloads/simpy-ep14.pdf).

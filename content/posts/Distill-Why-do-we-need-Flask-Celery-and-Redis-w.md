---
 	layout: post
 	title: Distill-Why-do-we-need-Flask-Celery-and-Redis-w
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# Distill-Why-do-we-need-Flask-Celery-and-Redis-w** In the next section, we’ll discuss the various components of Mcdonald’s task queue and how they map to the three technologies above.
## Diving into Mcdonald’s Task Queue
In the Mcdonalds near our office, there are three major components that are in play:
- **The *Ate*/*Kuya* cashier**: they’re the ones who talk to customers, take their orders, and give them their reference numbers *(remember that in the Mcdo near our apartment, they’re also the ones who prepares the meal, which is inefficient)*.
- **The database behind the LED screen**: the LED screen displays information on the customers’ reference numbers and order status, but we know that it’s job is to *only show* information.
The cashier takes their order, put it in the database queue (with a `PENDING` status), so that free workers can take them on.
[Distill%20Why%20do%20we%20need%20Flask,%20Celery,%20and%20Redis%20(w%204b3cfc055f3f44beb14348e7163ece7b/task_queue_02.svg](Distill%20Why%20do%20we%20need%20Flask,%20Celery,%20and%20Redis%20(w%204b3cfc055f3f44beb14348e7163ece7b/task_queue_02.svg)
We consider ourselves as the **[Client](https://en.wikipedia.org/wiki/Client%E2%80%93server_model)**, for we’re the ones asking for a service or making a **Request**.
- The components of the Mcdonald’s task queue: cashier, worker, database behind LED screen
- How these components look like in more general terms: application, worker, database backend.
The App takes the request, put it in the database queue (with a `PENDING` status), so that Celery workers can take them on.

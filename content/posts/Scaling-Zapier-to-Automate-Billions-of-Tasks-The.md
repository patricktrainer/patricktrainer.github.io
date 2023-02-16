---
date: '2023-02-16'
draft: false
title: Scaling-Zapier-to-Automate-Billions-of-Tasks-The
---

# Scaling-Zapier-to-Automate-Billions-of-Tasks-The

# Scaling Zapier to Automate Billions of Tasks - The Zapier Engineering Blog | Zapier
Created: June 18, 2020 3:54 AM
URL: https://zapier.com/engineering/automating-billions-of-tasks/
!
## The Teams Behind the Curtains
It takes a lot to make Zapier tick, so we have four distinct teams in engineering:
- The **frontend team** works on the very powerful workflow editor.
### Data
MySQL is our primary relational data store—you'll find our users, Zaps and more inside MySQL.
## Some Rough Numbers
These numbers represent a rough minimum to help the reader gauge the general size and dimensions of Zapier's architecture:
- over 8m tasks automated daily
- over 60m API calls daily
- over 10m inbound webhooks daily
- ~12 c3.2xlarge boxes running HTTP behind ELB
- ~100 m3.2xlarge background workers running Celery (split amongst polling, hooks, email, misc)
- ~3 m3.medium RabbitMQ nodes in a cluster
- ~4 r3.2xlarge Redis instances - one hot, two failover, one backup/imaging
- ~12 m2.xlarge Memcached instances behind ~6 c3.xlarge McRouter instances
- ~10 m3.xlarge ElasticSearch instances behind ~3 m3.xlarge no-data ElasticSearch instances
- ~6 m3.xlarge ElasticSearch instances behind ~1 c3.2xlarge Graylog server
- ~10 dc1.large Redshift nodes in a cluster
- 1 master db.m2.2xlarge RDS MySQL instance w/ ~2 more replicas for both production reads and analysis
- a handful of supporting RDS MySQL instance (more details below)
- …and tons of microservices and miscellaneous specialty services
## Improving the Architecture
While the broad strokes of the architecture remain the same—we've only performed a few massive migrations—a lot of work has been done to grow the product in two categories:
1.
Every step has to consume some data (which folder to read from or which list ID to add to, for example), do some API magic, and return some data (say, the new file created or the new card added to a list), but otherwise be ignorant of its placement in the workflow.
In the middle exists the omniscient workflow engine which coordinates independent Celery tasks by stringing together steps as tasks—one step feeding into the next as defined by the Zap's directed rooted tree.
In addition to Multi-Step Zaps, we've also launched the ability to write [Python](https://zapier.com/help/code-python/) and [JavaScript](https://zapier.com/help/code/) as Code steps in your workflow.

---
date: '2023-02-16'
draft: false
title: The-unreasonable-importance-of-data-preparation
---

# The-unreasonable-importance-of-data-preparation

When executives ask me how to approach an AI transformation, I show them Monica Rogati’s [AI Hierarchy of Needs](https://hackernoon.com/the-ai-hierarchy-of-needs-18f111fcc007), which has AI at the top, and everything is built upon the foundation of data (Rogati is a data science and AI advisor, former VP of data at Jawbone, and former LinkedIn data scientist):
!
## Data professionals spend an inordinate amount on time cleaning, repairing, and preparing data
Before you even think about sophisticated modeling, state-of-the-art machine learning, and AI, you need to make sure your data is ready for analysis—this is the realm of data preparation.
No data analysts/scientists work on this data pipeline as everything must happen in real time, requiring an automated data preparation and data quality workflow (e.g., to resolve if I say “eye-talian” instead of “it-atian”).
Understanding the importance of general automation and democratization of all parts of the DS/ML/AI workflow, it’s important to recognize that we’ve done pretty well at democratizing data collection and gathering, modeling[[8]](https://www.oreilly.com/radar/the-unreasonable-importance-of-data-preparation/), and data reporting[[9]](https://www.oreilly.com/radar/the-unreasonable-importance-of-data-preparation/), but what remains stubbornly difficult is the whole process of preparing the data.
## Modern tools for automating data cleaning and data preparation
We’re seeing the emergence of modern tools for automated data cleaning and preparation, such as [HoloClean](https://hazyresearch.github.io/snorkel/blog/holoclean.html) and [Snorkel](https://www.snorkel.org/) coming from [Christopher Ré’s group at Stanford](https://cs.stanford.edu/~chrismre/).
HoloClean decouples the task of data cleaning into error detection (such as recognizing that the location “cicago” is erroneous) and repairing erroneous data (such as changing “cicago” to “Chicago”), and formalizes the fact that “data cleaning is a statistical learning and inference problem.” All data analysis and data science work is a combination of data, assumptions, and prior knowledge.
Snorkel provides a way to automate labeling, using a modern paradigm called [data programming](https://arxiv.org/abs/1605.07723), in which users are able to “inject domain information [or heuristics] into machine learning models in higher level, higher bandwidth ways than manually labeling thousands or millions of individual data points.” [Researchers at Google AI](https://ai.googleblog.com/2019/03/harnessing-organizational-knowledge-for.html) have adapted Snorkel to label data at industrial/web scale and demonstrated its utility in three scenarios: topic classification, product classification, and real-time event classification.

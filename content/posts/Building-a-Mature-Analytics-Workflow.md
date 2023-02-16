---
date: '2021-01-01'
draft: false
tags: '[]'
title: Building-a-Mature-Analytics-Workflow
---

# Building-a-Mature-Analytics-Workflow

The center of gravity in mature analytics organizations has shifted away from proprietary, end-to-end tools towards more composable solutions made up of:
- data integration scripts and/or tools,
- high-performance analytic databases,
- SQL, R, and/or Python, and
- visualization tools.
We believe a mature analytics team’s techniques and workflow should have the following collaboration features:
### **Version Control**
Analytic code — whether it’s Python, SQL, Java, or anything else — should be version controlled.
>
If analytics is core to the success of an organization, the code, processes, and tooling required to produce that analysis are core organizational investments.We believe a mature analytics organization’s workflow should have the following characteristics so as to protect and grow that investment:
### **Environments**
Analytics requires multiple environments.
### Analytics workflows require automated tools
Frequently, much of an analytic workflow is manual.
Today, we’re announcing the release of the first version of our initial set of tools:
- **[dbt](https://github.com/analyst-collective/dbt) (data build tool)** is a deployment tool for data models.
Future versions of dbt will a) extend it to become a package management system, enabling an open source analytics ecosystem, b) automatically run tests on top of data models, and c) extend it to other analytic databases.
Analyst Collective is sponsored by [RJMetrics Pipeline](https://rjmetrics.com/product/pipeline), a tool that helps data engineers and analysts consolidate data into Amazon Redshift.

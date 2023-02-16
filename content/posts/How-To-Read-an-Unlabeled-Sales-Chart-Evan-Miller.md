---
 	layout: post
 	title: How-To-Read-an-Unlabeled-Sales-Chart-Evan-Miller
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# How-To-Read-an-Unlabeled-Sales-Chart-Evan-Miller# How To Read an Unlabeled Sales Chart – Evan Miller
Created: January 14, 2020 4:02 PM
Tags: Data, How To
URL: https://www.evanmiller.org/how-to-read-an-unlabeled-sales-chart.html
A genre of blog post that is perennially popular among independent software developers is “How My Sales Skyrocketed After…”, where for the ellipsis you my substitute any number of fortuitous events or marketing techniques.
As I pondered the blurred-out Y-axis in the above picture, a much more interesting topic occurred to me, and so I’ve decided to write about that instead: how to deduce the scale of a sales chart in which the Y-axis is missing.
## Technique #1: Counting Pixels and the Riemann Zeta Function
The first thing you might try is to measure the size of each bar in pixels and determine the greatest common divisor among all of the pixel counts.
If there is no common divisor among the sale counts, then greatest common divisor among the pixel counts will correspond to the number of pixels that represent a single sale.
## Technique #2: Properties of a Poisson Process
In the absence of calamity, fortuitous events, or brilliant new marketing strategies, sale counts are well-described by a Poisson process.
Assuming sales are a Poisson process, we can equate the sales mean to the sales variance:
S=i=1(SPi−S)2
Rearranging you get a nice equation for sales per pixel:
S=
Which could also be written:
S=
In plain English, the number of sales per pixel can be estimated as the average bar height in pixels divided by the variance of the bar heights.
To see how well this works in practice, I ran the numbers on the first 13 bars of the above chart (that is, before the sales spike, which interrupted the usual Poisson process).

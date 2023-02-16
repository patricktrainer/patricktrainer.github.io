---
 	layout: post
 	title: 2001-03147-Age-Partitioned-Bloom-Filters
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# 2001-03147-Age-Partitioned-Bloom-Filters# [2001.03147] Age-Partitioned Bloom Filters
Created: January 11, 2020 12:51 AM
Tags: Data
URL: https://arxiv.org/abs/2001.03147
> Bloom filters (BF) are widely used for approximate membership queries over a set of elements.
BF variants allow removals, sets of unbounded size or querying a sliding window over an unbounded stream.
However, for this last case the best current approaches are dictionary based (e.g., based on Cuckoo Filters or TinyTable), and it may seem that BF-based approaches will never be competitive to dictionary-based ones.
In this paper we present Age-Partitioned Bloom Filters, a BF-based approach for duplicate detection in sliding windows that not only is competitive in time-complexity, but has better space usage than current dictionary-based approaches (e.g., SWAMP), at the cost of some moderate slack.
APBFs retain the BF simplicity, unlike dictionary-based approaches, important for hardware-based implementations, and can integrate known improvements such as double hashing or blocking.
We present an Age-Partitioned Blocked Bloom Filter variant which can operate with 2-3 cache-line accesses per insertion and around 2-4 per query, even for high accuracy filters.
>

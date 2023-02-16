---
date: '2023-02-16'
draft: false
title: Simple-Fast-Easy-Parallelism-in-Shell-Pipelines
---

# Simple-Fast-Easy-Parallelism-in-Shell-Pipelines

# Simple, Fast, Easy Parallelism in Shell Pipelines
Created: January 12, 2023 9:28 PM
URL: https://catern.com/posts/pipes.html
The typical shell[1](https://catern.com/posts/pipes.html#fn.1) pipeline looks something like this:
Usually `src` will output lines of data, and `worker` acts as a filter, processing each line and sending some transformed lines to `sink`.
So there is a possibility of parallel processing on the basis of lines: We could have multiple `worker` tasks[2](https://catern.com/posts/pipes.html#fn.2) which each process different lines of data from `src` and output transformed lines to `sink`.
But the typical data-processing Unix command reads lines of input from stdin, not from its arguments on the command line, so many commands simply don't make sense to use with `xargs`.
A technique that allows a pool of worker tasks[2](https://catern.com/posts/pipes.html#fn.2), executing in parallel, to process incoming lines as they arrive on stdin, would be strictly more general.
Writing a parallel pipeline in any shell looks like this:[3](https://catern.com/posts/pipes.html#fn.3)
```
src | { worker &
worker &
worker & } | sink
```
This will start up three workers in the background, which will all read data from src in parallel, and write output to sink.
[5](https://catern.com/posts/pipes.html#fn.5)
Since all the worker tasks are reading input at the same time, we might run into a common concurrency issue: one worker task might get the first part of a line, while the rest of the line goes to another worker task.
We can control interleaving of the output with other techniques too, such as `stdbuf -oL`, to force output to be written in units of whole lines, which will be atomic as long as those lines are short enough.

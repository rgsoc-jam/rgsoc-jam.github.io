---
layout: post
title:  "Day 4: Our First Pull Request"
date:   2016-07-07
categories: [log]
comments: false
tags: [log]
authors: Jeena and Malisa
---

Yesterday we attended the PDX Rust meet-up and saw Andy Grover give a presentation on his project [Froyo](https://github.com/agrover/froyo).

Today we worked at the Portland Mozilla office to program on a really easy Servo issue just to get used to the workflow. With the help of our coach Nick we were able to submit our first pull request, which was accepted. :)

## Things we did:  
- Re-factored some code related to [Interval Profiling](https://github.com/servo/servo/wiki/Profiling#interval-profiling), specifically the calculation of the mean, median, minimum, and maximum of the time spent on various events. (Not related to the Fetch API, which is our main project.) The PR: [here](https://github.com/servo/servo/pull/12327).
- Upgraded Emacs configuration, e.g. `rust-mode`, and learned some best practices for using Emacs
- Implemented step one of [Headers.append()](https://fetch.spec.whatwg.org/#dom-headers-append) for the Fetch API (normalize), together with Nick.

## To-Do:
- Learn more Rust
- Implement more of the Headers methods
- Write tests for the append() method

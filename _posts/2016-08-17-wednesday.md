---
layout: post
title:  "Day 33: Moving at a Snail's Pace"
date:   2016-08-17
categories: [log]
comments: false
tags: [log, rust]
authors: Jeena and Malisa
---

## Things we did:
- Headers (Jeena)
  - Worked on including "content-type" in cors-safelisted-request-header.
  - Opened a [pull request](https://github.com/servo/servo/pull/12915)!
- Response (Malisa)
  - Finished up the constructor (as well as I can while we wait on entry settings object to be implemented and `promise` to get merged in).
  - Currently dealing with constructor build errors
  - still confused about how everything integrates together with the network-level stuff

## Things we learned:
- We are still a long ways off from understanding how Fetch works!

## TODO:
- Headers (Jeena)
    - Review `mime` and see if I can use it for the PR I opened today.
    - Refactor iterable implementation
- Response (Malisa)
    - Fix build errors
    - Try to understand network-level stuff

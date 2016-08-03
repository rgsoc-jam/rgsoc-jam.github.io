---
layout: post
title:  "Day 23: Just What I Needed"
date:   2016-08-03
categories: [log]
comments: false
tags: [log, servo]
authors: Jeena and Malisa
---

## Things we did:
- General
    - Started thinking about the blog post.
- Request API
    - Submitted a [PR](https://github.com/servo/servo/pull/12722) for enabling Request API and Response API tests, but tests are failing!
    - Started addressing comments from the Request API [PR](https://github.com/servo/servo/pull/12700).
- Response API
    - Still working on step 2 of the constructor. Ended up spending a lot of time understanding and testing how deref coercions and ownership works.

## Things we learned:
- [Deref coercions](https://doc.rust-lang.org/book/deref-coercions.html)

## TODO:
- General:
    - Write a blog post!
- Response:
    - Continue working on constructor.
- Request:
    - Troubleshoot what's going on with PR #12722.
    - Keep addressing comments.

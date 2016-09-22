---
layout: post
title:  "Day 56: Next Steps"
date:   2016-09-21
categories: [log]
comments: false
tags: [log, rust]
authors: Jeena and Malisa
---

## Things we did:
- Body
    - Submitted [PR](https://github.com/servo/servo/pull/13345) last night for dom::Response's Body::text function. Got back some feedback. Spent some of this afternoon planning the next steps.
- Blog
    - I (Malisa) spent some time writing my Strange Loop blog....will try to do some more coding tonight.
- Promise in Fetch
    - Addressed review comments from the [PR](https://github.com/servo/servo/pull/13323).
- OpenEndedDictionary in Headers
    - Opened a [PR](https://github.com/servo/servo/pull/13356) and addressed review comments.

## TODO:
- Body (Malisa)
    - Fix code based on jdm's feedback and refactor.
- Test Curation
    - Go through the new tests, and categorize them.
- Package Data Algorithm (Jeena)
    - We decided that I should work on implementing the rest of the package data algorithm. This decides what to do given a Body, depending on its type (a text, json, and etc). Malisa already implemented text, so that's great! Malisa will focus on going through review comments from her recent PR, and refactoring `consume_body` and making it into a public function. That way, it can be called by both Request and Response. At this moment, `consume_body` is customized for Response specifically, and it will be redundant to do the write the same function for Request.

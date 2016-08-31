---
layout: post
title:  "Day 42: Purrling"
date:   2016-08-31
categories: [log]
comments: false
tags: [log, servo]
authors: Jeena and Malisa
---

[Purrling](http://i.imgur.com/EbolG1m.gifv)*

## Things we did:
- Response
    - Fixed minor error: Status method should return net_traits::Response's raw_status's status, not net_traits::Response's status.
    - Learned that it might be a good idea to refactor the code and remove the use of net_traits::Response altogether from dom::Response. There are pros and cons to this.
- Test Curation
   - Opened an [issue](https://github.com/servo/servo/issues/13144) about OpenEndedDictionary support
   - Spent most of the day learning about http.

## Things we learned:
- How to think about sockets: HTTP request/response are sent via TCP. TCP connections use sockets.

## TODO:
- Body
    - Start implementing body for Response and Request
- Promise in Fetch
   - After few trial and error, as long as `Fetch.webidl` states that it returns a `void` (not `Promise`), the code compiles! I’ll keep building on top of it...

* absolutely not work-related

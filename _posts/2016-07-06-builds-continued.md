---
layout: post
title:  "Day 3: Builds Continued"
date:   2016-07-06
categories: [log]
comments: false
tags: [log]
authors: Jeena and Malisa
---

## Things we did:  
- Had a kick-off call to say [hi](https://pics.onsizzle.com/Instagram-PIZZA-86ce5e.png), discuss various logistics, and the best way to ramp up to speed on Servo
    - We are planning on spending Thursday working on an E-Easy tagged Servo issue with our coaches, just to get used to the workflow
    - In terms of dividing our time between learning Rust and working on Servo, the consensus was that it is good to know enough Rust to understand basic Servo code, but it is also important to dive into the issues!
- Decided to do work on our own Servo forks as opposed to a team fork. Learned how to reset our working repo to a particular fork, branch, or commit.
- Ran into more build issues. Oddly, the build that worked for us yesterday didn't work for us this morning. After some troubleshooting we got it to run again. In the process we learned:
    - Learned that we need to add `#[dom_struct]` before our `headers.rs` `struct` declaration, and the first field of the `struct` has to either be a Reflector or the object it inherits

## To-Do:
- Go to the Rust PDX meet-up tonight!
- Learn more Rust
- Ask Josh how often to pull from Servo (pulling and re-building every day might result in a significant amount of our time spent dealing with build failures)
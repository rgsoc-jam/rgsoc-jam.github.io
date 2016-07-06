---
layout: post
title:  "Day 2: Building Blocks"
date:   2016-07-05
categories: [log]
comments: false
tags: [log]
authors: Jeena and Malisa
---
We had a nice long Independence Day weekend and are happy to be back coding on Servo!

## Things we did:  
- Added skeleton code for the Headers API (part of the Fetch API)
- Ran into [PR issue #12271](https://github.com/servo/servo/pull/12271) while building the code on both Ubuntu 14.04 and OSX, indicating that the bug was a more general issue than it was originally thought to be
- Learned that rebuilding Servo after making code changes sometimes requires running the `./mach clean` command in order to clear the "build cache" prior to running `./mach build --dev`
- Applied for RustConf scholarships
- Looked into optimal git workflow for Servo and RGSoC

## To-Do:
- Learn more Rust
- Finish implementing the Headers API skeleton, as well as the Request and Response API skeletons
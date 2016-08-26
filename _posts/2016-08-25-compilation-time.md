---
layout: post
title:  "Day 38: Dancing the Compilation Dance"
date:   2016-08-25
categories: [log]
comments: false
tags: [log, servo]
authors: Jeena and Malisa
---
Like this!

![robot-dance](/img/robot-dance.gif)

## Things we did:
- Fetch
    - Set up the skeletons for Fetch. It was a tricky process. Fetch is defined in `WindowOrWorkerGlobalScope.webidl` which is a newer addition to the spec and was not present in Servo. I had to add it to Servo, and `WindowOrWorkerGlobalScope` is not a interface object, so no bindings were created. The compiler told me that `dom/window.rs` and `dom/workerglobalscope.rs` had to implement `Fetch()`. So what we decided to do is have a `script/fetch.rs` where the Fetch method will live, and have `dom/window.rs` and `dom/workerglobalscope.rs` delegate the Fetch method to `script/fetch.rs`.
- Response
    - Ended up having to replace instances of `RawStatus` (which takes a utf-8 encoded Cow-str) in Servo's codebase with `(u16, Vec<u8>)`, which is not UTF-8-dependent. I spent the whole day re-building and finding new places in the codebase which were affected by this change, fixing, and re-building again! Finally the relevant test is passing though :)

## Things we learned:
- Don't spend too much time trying to predict the repercussions of a change in your Rust code. (I do this a lot - Malisa) Often-times the Rust compiler will tell you what those repercussions are, and save you a lot of time, even though you might get surprised by some unexpected errors while building your project!

## TODO:
- Fetch
    - It seems like a huge chunk of Fetch is already implemented in `net/fetch/method.rs`. Figure out how to wrap `script/fetch.rs` around `net/fetch`.
- Response
    - update tests, clean up code, and submit the PR already!
- Miscellaneous
    - Publish a blog post about move, clone, and copy! (Jeena)
    - Before Josh goes on a vacation, ask him what we should work on next week.

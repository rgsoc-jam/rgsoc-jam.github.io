---
layout: post
title:  "Day 55: Oooo another exciting day"
date:   2016-09-20
categories: [log]
comments: false
tags: [log, rust]
authors: Jeena and Malisa
---

## Things we did:
- OpenEndedDictionary in DOM (Jeena)
    - Ms2ger [implemented](https://github.com/servo/servo/pull/13332) OpenEndedDictionary! This is what will allow more Headers/Request/Response tests to pass. Woohoo!
    - So I modified our Headers and Request APIs to adapt to this change. I fought with the borrow checker a lot today, but overall, it was successful. Thanks rustc!

- Body
    - Got dom::Response's Body `text()` function to the point that it compiles, but additional tests are not passing. I keep getting the same error `Promise is not defined` in testharness.js.

## Things we learned:
- When `T` doesn't derive clone, or has a clone implementation, the compiler makes another reference when `.clone()` is called to a `&T`, ending up with `&&T`. When `.clone()` is called, the compiler derefs `&T` to `T`, realizes `T` cannot be cloned, and so it creates a clone to the reference, hence creating a double reference.

## TODO:
- Promise in Fetch
    - Go through failing tests and figure out what I can fix.
- Test Curation
    - Go through the new tests, and categorize them.
- OpenEndedDictionary in DOM
    - Is it time for a PR?
- Body
    - Figure out whether I have a bug. Ask jdm. Then submit PR.

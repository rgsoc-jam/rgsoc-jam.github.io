---
layout: post
title:  "Day 62: D-1: Body and Fetch, woo! hoo!"
date:   2016-09-29
categories: [log]
comments: false
tags: [log, servo]
authors: Jeena and Malisa
---
We're having our end of summer party. We're going to see thousands of swift birds fly into a chimney for the night! So excited.

## Things we did:
- Body
    - Body mixin methods are [now supported](https://github.com/servo/servo/pull/13345)!
- Fetch
    - Fetch method is [now supported too](https://github.com/servo/servo/pull/13323)!
- Malisa
    - Spent the morning categorizing `fetch/api/basic` tests. >90% of failing tests were due to `fetch is not defined`. The remaining two failures were due to `assert_equals: Request.text() should decode data as UTF-8` and `assert_equals: Response.text() should decode data as UTF-8 expected`.  In the afternoon fetch got merged into master, so I retested `response` and `basic` at that point....now there is a lot of `assert_equals: Request.text() should decode data as UTF-8 expected` and `assert_equals: Response's type is basic expected "basic" but got "default"`. Started trying to figure out what's wrong with body's `text()` Looked into `request/request-consume.html` and `/basic/text-utf8.html`....not sure how to fix!
- Jeena
    - Started writing a blog post that is a secret yet!

## TODO:
- Test Curation
    - Possibly update because fetch and body are now merged.

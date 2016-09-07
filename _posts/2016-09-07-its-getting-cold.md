---
layout: post
title:  "Day 45: Dear Promise, please promise me you'll be complete one day. Love, jam"
date:   2016-09-07
categories: [log]
comments: false
tags: [log, servo]
authors: Jeena and Malisa
---

Yesterday was Labor Day, so we celebrated it by not working! Woohoo! Malisa is traveling back today, so I (Jeena) worked alone today.

## Things we did:
- Promise in Fetch
    - jdm is back! He rebased his promises branch! :clap: The rust compiler still [panics instead of throwing error](https://github.com/rust-lang/rust/issues/36092) as it uses the older rust version, but that's ok! I can work around it.
    - It turns out there's a lot more to do with implementing promise in `fetch` so I spent the day trying to understand what I need to do. Roughly, there are two things I can do:
        1. figure out how to reject/resolve Promise in `fetch`. `Promise::maybe_resolve_native` is probably a better choice than `Promise::maybe_resolve` because they take regular DOM objects. This seems partially dependent on the next thing.
        2. implement `FetchResponseListener` in `fetch.rs`. This turns out to have a lot more pre-requisite infrastructure! `fetch.rs` needs a `FetchContext` struct that will store the intermediate fetch. `XMLHttpRequest` is done very similarly to `fetch`, so I should look into how XHR is implemented in Servo. How XHR implements `FetchResponseListener` is [here](https://doc.servo.org/src/script/dom/xmlhttprequest.rs.html#222-252).

## Things we learned:
- jdm drew a great [diagram describing how `XMLHttpRequest` interacts with resource thread and `XHRContext`](http://www.joshmatthews.net/diagram.svg)
- Promise doesn't have to be rooted! <small><i>Whaaaat.</i></small> jdm says "Rc<SomeDOMType> would usually be unsafe but Promise is designed in such a way that it's safe, whereas Rooted<Promise> would be incorrect." <small><i>Whaaaat?</i></small> I don't even understand! We'll find out the reason later...

## TODO:
- Promise in Fetch
    - make `FetchContext` struct
    - `Impl FetchResponseListener for FetchContext` (may require helper functions)
    - resolve/reject promise in fetch

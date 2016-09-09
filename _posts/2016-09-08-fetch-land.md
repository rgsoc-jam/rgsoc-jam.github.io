---
layout: post
title:  "Day 47: jammin' the fetch"
date:   2016-09-08
categories: [log]
comments: false
tags: [log, rust]
authors: Jeena and Malisa
---

## Things we did:
- Miscellaneous
    - Today we had a monthly meeting with everyone, and it was gooood :+1:. Special thanks to Scott for the pep talk! Also, we picked and ate [figs from the fig tree](http://imgur.com/X5FGlgZ?r) by Jeena's home as a break :deciduous_tree:.

- Promise in Fetch
    - Today was indeed a different day! I started working on implementing the `FetchResponseListener`. `FetchResponseListener` is invoked when (I think) the network level fetch gets some data back. For example, a method in `FetchResponseListener` is `process_response`, which will update the response object with the data it got back from fetching.
    - Josh suggested not worrying about the FetchContext, which will be the struct to hold promise and response together, until later. Creating the FetchContext will require a lot of wrappings.
        - The fetch listener (`FetchContext`) has to be `Arc<Mutex<T>>`. Inside `FetchContext`, there will be `response_object` with type `Response` and `promise` with type `Rc<Promise>`. Both `response_object` and `promise` will need to be wrapped with `Trusted` to be shared across threads safely. `Trusted` is a "safe wrapper around a raw pointer to a DOM object", so `response_object` and `promise` can be `Trusted<Response>` and `Trusted<Promise>`.
        - I think `response_object` should be wrapped wtih `DOMRefCell` to allow inner mutability, but we shall see. If this is true, `response_object` will be `DOMRefCell<Trusted<Response>>`..? Josh said that since FetchResponseListener will be implemented on FetchContext, calling `self.response_object.root()` will obtain a `Root<Response>` value in the callbacks that can be manipulated like usual.
        - `promise` is `Rc<T>` so we will need a method that will pull out `Rc<T>` from `Trusted<T>`, like `self.response_object.root()` would.

- Body
    - Wrote step 34 of Request constructor to extract Body contents. The [extract body method](https://dxr.mozilla.org/servo/source/components/script/dom/xmlhttprequest.rs?q=path%3Axmlhttprequest.rs&redirect_type=single#1352) still doesn't use ReadableStream so I'm not sure if it will need to be rewritten.
    - Step 7.3 of Response

## Things we learned:
- The difference between Mutex types and regular-ol'-mutable-rust-variables. Both only allow mutation of their data one thing at a time, through either `& mut` or for mutex `lock()` and `unlock()`. What makes [Mutex](https://doc.rust-lang.org/std/sync/struct.Mutex.html) special? It is specifically designed for sharing across threads (often used in conjunction with Arc), whereas regular mutable borrow is not. So, only one thread can safely access the same data at one time. On the other hand, regular-ol'-`& mut` will not be allowed by the borrow checker if you try to use it across threads.
- A whole lot about network-level fetch! Network level fetch is the communication with the core resource thread that invokes fetch algorithms, as described in [the spec](https://fetch.spec.whatwg.org/#fetching). There are a couple Servo parts that already use the network-level fetch: [XMLHttpRequest](https://doc.servo.org/src/script/dom/xmlhttprequest.rs.html#218-252) and [script](https://github.com/servo/servo/pull/12472/).
- `Rc<T>` is not thread-safe, but `Trusted<T>` is, like in `Trusted<XMLHttpRequest>`.

## TODO:
- Promise in Fetch
    - make FetchContext struct (on hold)
    - Impl FetchResponseListener for FetchContext (may require helper functions)
    - resolve/reject promise in fetch (figure out how to use `maybe_reject_error`, etc.)
- Body
    - implement the rest of the body interface for dom::Response

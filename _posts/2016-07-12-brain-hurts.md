---
layout: post
title:  "Day 7: Our brains hurt from learning so much"
date:   2016-07-12
categories: [log]
comments: false
tags: [log, rust, servo]
authors: Jeena and Malisa
---

## Things we did:
- Re-organized a lot of our validate function we wrote yesterday.
    - We had misinterpreted the HeadersAPI spec. We were thinking way too far ahead.
    - But, the code we wrote yesterday will be useful in the near future, so :thumbsup:.
- We understood better what we need to do for validating Header name and value.
    - We will have to write parsers to do so.
- Started writing different components for the parsers.
- We added `guard` to our `Headers` struct.
- We created `enum Guard` for `guard`.
- We got a lot of practice using `Result<>`.
- We filed an [issue] (https://github.com/whatwg/fetch/issues/332) at whatwg/fetch.

## Things we learned:
- How to add crate dependencies (assuming `script` is the root directory of our files):
    - In `components/script/lib.rs`, add `extern crate unicase;`.
    - In `components/script/Cargo.toml`, add `use unicase="1.4.0"`.
- `Cow` automatically handles copy and writing when you have a borrowed immutable reference.
- Emacs tip "defining macro":
    - `C-x (` (define macro) `C-x )` `C-e` (execute macro)
- `String` is guaranteed to be UTF8 and is heap-allocated (and therefore growable). `&str` is a `string-slice`. `dom::bindings::str::ByteString` is not guaranteed to be UTF8.
- If `Result` only returns an error, use `Result<(), Error>`.
- For Boolean matching in Rust, use `&&`.
- Because the Headers API interacts with JS, JS garbage collector must be able to trace Headers API's elements. In order to allow that, above a struct or enum that declares, add `#[derive(JSTraceable, HeapSizeOf)]`.
- Crate `regex` supports pattern matching on bytes. Add `use regex::bytes` to the code.

## TODO:
- Finish writing field name and field content parsers.
- Figure out how to wrap our Headers struct around `hyper::headers::Headers`. Ask jdm!
- Continue writing `Append` method.

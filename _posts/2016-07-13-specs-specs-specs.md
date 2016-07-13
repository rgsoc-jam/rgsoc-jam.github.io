---
layout: post
title:  "Day 8: Specs Specs Specs!"
date:   2016-07-13
categories: [log]
comments: false
tags: [log, servo]
authors: Jeena and Malisa
---

## Things we did:
- Had a weekly call with Scott. Everything's great so far!
- Navigated through HTTP, and its list of errata. Found out the issue we filed yesterday might have been resolved through [Errata ID: 4189](http://www.rfc-editor.org/errata_search.php?rfc=7230).
- Finished writing field name and field content parsers.
- Figured out how to wrap our Headers struct around `hyper::headers::Headers`.
    - In Headers struct, added `header_list: hyper::header::Headers`.
    - Had to add `#[ignore_heap_size_of = "Defined in hyper"]`.
- Wrote steps 3-6 for [append](https://fetch.spec.whatwg.org/#headers) method.

## Things we learned:
- `*ByteString` -> `[u8]`
- `&` creates a slice of a view of some number of elements
- `&(*ByteString)` -> `&[u8]`
- But! `&*(&ByteString)` -> `&[u8]`
- `Cow` derefs to `str` (needs double checking).
- How to do regex matching on bytes in Rust (check for one or more of space or tabs):
    - `bytes::Regex::new(r"(\x20|\x09)+?").unwrap().is_match(&u8)`
- Function to remove HTTP whitespace was already [written](http://doc.servo.org/src/net_traits/lib.rs.html#674-696) in Servo! Though we don't know if `ByteString` will be a valid input type, so we'll just keep this knowledge in the back of our mind.

## TODO:
- Implement `new()` for our Headers struct.
- Finish up writing `Append`.
    - Probably should use `set`.
    - As `set` requires the header name (which is a `ByteString`) to implement `Into<Cow<'static, str>>`, we might have to implement it ourselves (`impl Into<Cow<'static, str>> for ByteString`).
- Write tests for the parsers.
- Write function that will parse header value.

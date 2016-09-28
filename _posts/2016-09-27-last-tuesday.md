---
layout: post
title:  "Day 60: D-3: Only 3 days until last day"
date:   2016-09-27
categories: [log]
comments: false
tags: [log]
authors: Jeena and Malisa
---

## Things we did:
- Body
    - Started fixing the Body implementation based on jdm's feedback
    - Filed issue [#13465](https://github.com/servo/servo/issues/13465) related to allowing trait object in promise.rs.
    - Filed issue [#13464](https://github.com/servo/servo/issues/13464) about rethrowing exceptions instead of clearing pending JS exceptions in Body's `Json()` method.
    - The error we were getting was due to having an error in the webidl! We should have used `Primse<any>` instead of `Promise<JSON>`.
    - Looked into [form data crate](https://mikedilger.github.io/formdata/formdata/index.html) for parsing Form Data. `formdata::read_formdata` requires a reader, and I'm not entirely sure how we can use this parser without stream or HttpReader.
- General
    - We had lunch with Coach Stefan! :clap: We started thinking about what to do after this Friday when the summer of code is over...
    - We finished writing our end-of-summer blog post.
    - We went over the fetch method code to understand it better.
    - I wrote a [blog post about Strange Loop](http://jeenalee.com/2016/09/27/strange-loop.html) (Jeena).
    - Tonight, we're going to [Donut.js](http://donutjs.club/)!

## Things we learned:
- [Trait object in Rust](https://doc.rust-lang.org/book/trait-objects.html). Trait objects are the difference between `fn foo(object: &Trait)` (this is trait object) and `fn foo<T: Trait>(object: &T)`. The former will result in the compiler generating less code, so the compile time will be faster. However, this puts a little more strain during run time, because it will have to check whether the parameter object implements the `&Trait`. The latter generates more code during compilation because it will create unique functions for each type that implements `Trait`. This saves time during run time because the functions for each type is already defined. As Josh said "classic tradeoff between time and space!"

## TODO:
- Body
    - Continue fixing code for PR!
- Test Curation
    - Go through the new tests, and categorize them.

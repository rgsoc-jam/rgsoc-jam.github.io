---
layout: post
title:  "Day 28: Blast From the Past"
date:   2016-08-10
categories: [log]
comments: false
tags: [log, servo]
authors: Jeena and Malisa
---

## Things we did:
- Had our monthly meeting with everyone! Everyone is doing well. :D
- Blast from the past! Back to Headers API.
    - With the help of Stefan and [the rust playground](https://play.rust-lang.org/), we realized there were bugs in the `is_field_content` and `Append` functions in the Headers API. After [fixing these](https://github.com/servo/servo/pull/12700/commits/e8ace04b900d0081c4b22c55e61bf01837de9a4b), more of the Headers API tests passed! Oops...
- Response API/CodegenRust
    - Received feedback on bindings generator [PR](https://github.com/servo/servo/pull/12790). Once merged in, these changes will allow me to move forward with Response WebIDL implementation.
    - Drew a flowchart/diagram to understand each step of the response API.
- Request API
    - Realized that the reason Request tests fail is (at least partially) related to Headers not properly working.
    - Currently it looks like the Headers object is not properly created, or `Headers::Get` does not get the correct value.
- Had bubble tea

## Things we learned:
- `--log-mach /path/to/log/output` can be added when running servo tests to see verbose output and println's, for help in debugging
- Remember to build after making changes and before running tests!!! ;)

## TODO:
- Response:
  - Continue with Response constructor. Maybe, just maybe, be done with the constructor by Friday?
  - Figure out how to connect the two headers_list instances in the Response constructor using Rc.
- Request:
    - Debug the :poop: out of Headers.
- General:
    - Finish up writing blog post, intro to Rust's ownership.

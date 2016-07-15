---
layout: post
title:  "Day 10: Append is Almost There"
date:   2016-07-15
categories: [log]
comments: false
tags: [log, servo, rust]
authors: Jeena and Malisa
---

## Things we did:
- Submitted [PR#2](https://github.com/servo/servo/pull/12467) for code review, the append method for the Headers API. The code compiles on our machines locally but seems to fail Travis CI on github. Our coach @jdm also gave us a lot of good feedback which we are working through.
- Spent the afternoon brushing up on Rust!

## Things we learned:
- Debugging: Rust is a compiled language, so code needs to be built before running it. This means that you can get errors at two different stages, compile-time and runtime. As opposed to an interpreted language like Python where errors are found as each line of code is executed in order (top-to-bottom), Rust code is parsed in its entirety during compilation and different types of errors are found in stages. Python debugging is like a straight celery stick, and Rust debugging is more like an onion, with layers. One side-effect of this is that when we build Servo, the errors do not appear in a "linear" fashion, and fixing one bug at line 20 does not mean that lines 1-19 are perfect.
- Reflectors! For the past two weeks we have been mystified by the presence of Reflectors in Servo [DOM objects](https://doc.servo.org/script/dom/#a-dom-object-and-its-reflector). Today we learned that [Reflectors](http://doc.servo.org/script/dom/#reflector-and-reflectable) are JS objects allocated by SpiderMonkey (Mozilla's JS engine), that "reflect" the containing Rust object. An example of its use is [here](https://github.com/servo/servo/blob/master/components/script/dom/webglobject.rs#L12). This concept is hard to digest at first because it is circular: the JS reflector is embedded within the Rust DOM object, yet has a reference to the DOM object.

## TODO:
- Address all the feedback from PR#2, including a lot of refactoring and adding a `new_inherited` method (somewhat related to Reflectors).
- Should we write tests for our append method and associated helper functions?
- Come to a conclusion regarding the field-content production, i.e. [here](https://github.com/whatwg/fetch/issues/332).

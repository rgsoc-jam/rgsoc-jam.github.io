---
layout: post
title:  "Day 50: Jammin' Open Source"
date:   2016-09-13
categories: [log]
comments: false
tags: [log, rust, servo]
authors: Jeena and Malisa
---

Day 50! Today was a good day. We listened to our mentor Josh give a great talk about [Optimizing your project for contribution](http://www.oreilly.com/pub/e/3790). As mentees, we really appreciate all the work that's put into making Servo accessible to beginners.

## Things we did:
- Promise in Fetch
    - So yesterday, we found that `JSCompartment::wrap` had a parameter with a null pointer, which was the reason Servo was crashing. Josh recommended looking at dom/testbinding.rs to see how JSAutoCompartment is used, and to copy it in fetch.rs. After a little bit of wrestling with fetch.rs (because I mistakenly looked at the wrong code), [fetch, at least for now, works](/img/20160913-fetch.png)!
        - Some more explanation on JSCompartments is at the Today We Learned section. What was happening yesterday with the null pointer was that `promise` didn't enter any compartment, because `JSAutoCompartment::new()` wasn't called. `promise` had not entered any compartment, and therefore, when SpiderMonkey (JS Engine) called `JSCompartment::wrap()`, which would take a JSContext to the compartment of a JSObject, a null pointer was given. Apparently in order to enter a compartment, JSContext has to already have entered a compartment. And that's why Servo crashed!
        - We had been doing systems programming for two months, and this was our first time encountering a null pointer (which was in C++ code). Nick said that this shows how safe Rust is, because Rust would not have compiled in the first place. I haven't programmed in C++, but it must be annoying if a code compiles and so much time could pass until you find a memory pointer bug.
    - I submitted a [PR to enable fetch API tests](https://github.com/servo/servo/pull/13260) which will be useful in the (hopefully near) future.
- Body
    - I still didn't get a lot of code-writing done, but I have a better idea of where I'm headed now. I was unsure how closely I should be following the spec for utf-8 decoding. I asked jdm, and it turns out the answer is "just closely enough" (my own words).  So that's good, and I think I'm starting to understand how to not get super caught up in spec-reading loops of infinite link-following. It also turns out I can make use of the [encoding crate](https://doc.servo.org/encoding/index.html), which I believe means a lot of the actual decoding part has already been written for me.

## Things we learned:
- Spider Monkey specific: What is [JSAutoCompartment](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey/JSAPI_reference/JSAutoCompartment)? JSAutoCompartment helps a JSContext to enter a compartment, and leave the compartment when it is out of scope.
- Spider Monkey specific: What is a Compartment? Every JSContext has a *current* Compartment, but it won't enter its current compartment until `JSAutoCompartment::new()` is called. In a browser, one tab (one window) will have at least one compartment. Two tabs will have at least two compartments. Compartment is important for security, because there can be little cross-over that will be strictly controlled. You wouldn't want data jumping back and forth between different compartments.

## TODO:
- Body
    - continue with [UTF-8's decoder](https://encoding.spec.whatwg.org/#utf-8-decode). Now I really need to flesh out the code.
- Fetch Tests
    - It's time to go through the failing tests and see how to improve fetch.rs!
{% highlight console %}
Ran 104 tests finished in 100.0 seconds.
- 53 ran as expected. 0 tests skipped.
- 2 tests crashed unexpectedly
- 4 tests timed out unexpectedly
- 48 tests had unexpected subtest results
{% endhighlight %}

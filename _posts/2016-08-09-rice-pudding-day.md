---
layout: post
title:  "Day 27: Happy Rice Pudding Day!"
date:   2016-08-09
categories: [log]
comments: false
tags: [log, servo, emacs]
authors: Jeena and Malisa
---

## Things we did:
- Response API/CodegenRust
    - Added `p_ConstValueByteString` function to WebIDL.py and modified CodegenRust.py. Currently dealing with build errors.
- Request API
    - The Fetch spec was [updated](https://github.com/whatwg/fetch/pull/359). I updated the Request API script ro reflect the newest version of the spec.
    - Josh gave me more reviews, and I fixed the code.
    - But the tests are failing!! WHY! Why? why.........

## Things we learned:
- Learned a little about [`lex` and `yacc`](http://www.dabeaz.com/ply/ply.html) for string parsing, with the help of Nick.
- valid Python code using doc comments:

{% highlight python %}
>>> def add(a, b):
...     """Adds a to b"""
...     return a + b
...
>>> add(1, 2)
3
>>> add.__doc__
'Adds a to b'
{% endhighlight %}

- To go to a specific line in Emacs: `M-g g`, then enter line number. :tropical_drink:

## TODO:
- Response:
  - Continue with Response constructor again! Try to understand the context of what's going on as I do it.
- Request:
    - Figure out why tests are failing and fix the code.
- General:
    - Finish up writing blog post, intro to Rust's ownership.

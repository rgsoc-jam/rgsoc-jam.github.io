---
layout: post
title:  "Day 5: Going over Rust's Ownership and Borrowing"
date:   2016-07-08
categories: [log]
comments: false
tags: [log, rust]
authors: Jeena and Malisa
---

## Things we did:
- Reviewed Rust's [Ownership] (https://doc.rust-lang.org/book/ownership.html) and [Borrowing] (https://doc.rust-lang.org/book/references-and-borrowing.html).
- After reviewing, went through each line of the normalize function from yesterday.

## Things we learned:
- In Rust, only one thing can own a mutable reference at a time.
- Many things can have a reference to another thing, but only if it's an immutable reference.
- Dereferencing is a tricky concept. It can also be done in a couple different ways. For example two code snippets below would do the same thing:
{% highlight rust %}
      for byte in &value[first_index..last_index + 1] {
                        normalized_value.push(*byte);   // dereferencing here
                        }
{% endhighlight %}

{% highlight rust %}
      for &byte in &value[first_index..last_index + 1] { // destructuring here
                        normalized_value.push(byte);
                        }
{% endhighlight %}

## TODO:
- Learn more Rust (always!)
- Implement more of the Headers methods
- Write tests for the append() method
    - Finish writing test for normalize function

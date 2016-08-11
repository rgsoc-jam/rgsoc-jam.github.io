---
layout: post
title:  "Day 29: Happy Debugging"
date:   2016-08-11
categories: [log]
comments: false
tags: [log, servo, rust, fetch]
authors: Jeena and Malisa
---

## Things we did:
- Response API/CodegenRust
    - Small [PR](https://github.com/servo/servo/pull/12790) for default bytestring values in dictionaries got merged
    - Spent most of the day trying to figure out how to best make references between objects within the `Response` struct.
- Request API
    - Turns out I had to debug the :poop: out of Request, not Headers!
    - Fixed a bug. More in depth description below.
    - More tests are passing! I updated the expected test results.

## Things we learned:
- How to use reference-counted boxes: [`Rc<>`](https://doc.rust-lang.org/std/rc/#examples). They are a way to refer to the same internal object in multiple places. Different from `RefCell`, which I believe is more of a way to provide mutability of already-borrowed objects.

- When debugging a Rust code, you can print the memory address of the object through:
{% highlight rust %}
let x = 5;
println!("{:p}", &x);
{% endhighlight %}

- Approach debugging as if performing a scientific experiment. Do you have a hypothesis where it might be breaking? Sprinkle some print statements in the code, or set breaking points in the debugger. Study the results. Can you find a pointer that would lead to the next hypothesis? Repeat! And don't get frustrated!

*A Fun Debugging Tale*
Below is the test that was failing, and I was debugging:
{& highlight js %}
test(function() {
  var initialHeaders = new Headers([["Content-Type", "potato"]]);
  var initialRequest = new Request("", {"headers" : initialHeaders});
  var request = new Request(initialRequest);
  assert_equals(request.headers.get("Content-Type"), "potato");
  }, "Request should get its content-type from the init request");
{% endhighlight %}

The test creates an `initialRequest` with `initialHeaders`, and creates a `request` with the `initialRequest`. Then tries to assert that `request` has the same Headers as the `initialHeaders`. For some reason, `request`’s Headers becomes an empty object, so I was trying to figure out why.

[Here](https://fetch.spec.whatwg.org/#request-class) is the spec for constructing a Request object. `request`’s Headers is emptied at Step 29. It gets filled with `headers_copy` at Step 31. It turns out `headers_copy` was empty, and therefore at Step 29, the `request`’s Headers was getting filled with an empty Headers object.

`headers_copy` is set at Step 28. It states "If init's headers member is present, set headers to init's headers member.” It turns out that init’s headers didn’t exist when `request` was constructed. But it did exist when `initialRequest` was constructed.

So I had a hunch that maybe it was mixing up init and input. Constructor takes `input: RequestInfo` and `init: &RequestInit`. I printed out `input.headers`, and it was the same as `initialHeaders`. Once I added another logic in Step 28 to match input to Request and set `headers_copy` to input.headers, the test passed! I guess it was the cause for a few other tests to fail, so more tests are passing now. :raised_hands:

## TODO:
- Response API:
    - Update [`net_traits::Response`](https://github.com/servo/servo/blob/master/components/net_traits/response.rs#L87) and `net_traits::Request` and `dom::headers::Headers` to wrap `Rc<>` around their internal `hyper::header::Headers` objects. That way they will be clonable into reference-counted boxes.
    - After that hopefully I can actually do work on the Response constructor....fingers crossed...
- Request API:
    - Figure out whether I should file a Fetch spec bug.
- General:
    - Finish up writing blog post, intro to Rust's ownership.

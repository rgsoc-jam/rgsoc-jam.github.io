---
layout: post
title:  "Day 9: Nitty Gritty Details"
date:   2016-07-14
categories: [log]
comments: false
tags: [log, servo, rust]
authors: Jeena and Malisa
---

## Things we did:
- Implemented `new()` for our Headers struct.
- Added `append_the_header` method.
- Started writing `Append`, i.e. putting every helper function together. Wrote if/then logic for going through `Append` method.
- Ran into a lot of incompatible type issues. And we are still learning! :) :) :)
- We decided to be more aware of each other when pair programming. :D
- Used `DOMRefCell` instead of `RefCell` because `DOMRefCell` implements `JSTraceable`. With `RefCell`, the compiler threw an error saying it requires JSTraceable implementation.
- The reason we need `RefCell` is that it allows interior mutability to immutable borrowed content. The `header_list` needs to be mutated while auto-generated `HeadersBindings.rs` will borrow `Headers` immutably.

## Things we learned:
- `return` can only return from the current function, i.e. you can't return from an enclosing function in a closure.
- `match` doesn't introduce a new function or closure, so it is fine to return from a match arm
{% highlight rust %}
match x {
    Ok(value) => y = x,
    Err(e) => return Err(e),
}
{% endhighlight %}
- `try!` is awesome. Below two snippets would do the same thing.
{% highlight rust %}
try!(something_that_returns_a_result())
{% endhighlight %}

{% highlight rust %}
match something_that_returns_a_result() {
    Ok(v) => v,
    Err(e) => return Err(e),
}
{% endhighlight %}
- It is even possible to save what comes out of `try!` without unpacking `Ok()`:
{% highlight rust %}
let result_of_function = try!(something_that_returns_a_result());
{% endhighlight %}
- `'static` is either (1) a reference that is valid for the whole program's runtime, or (2) an owned pointer.

## TODO:
- Finish up writing `Append`.
- Refactor the code to look cleaner.
- Handle UTF8 conversion errors. (Also ask for second/third opinions on current implementation.)
- Write tests for the parsers.
- Write function that will parse header value.

---
layout: post
title:  "Day 18: Chugging Along"
date:   2016-07-27
categories: [log]
comments: false
tags: [log, servo]
authors: Jeena and Malisa
---

## Things we did:
- Request API
    - Wrote a couple helper methods for finding associated and current url, given a url list.
    - Started writing constructor step 13.

- Headers API
    - Finished up the remaining functions defined in the webidl. My job was made easier because I don't need to implement `iterable<ByteString, ByteString>` just quite yet.

## Things we learned:
- Even though the result of the two code blocks below are the same in practice, it's only due to the rust optimizer.

This first version only ever deals with one memory location on the stack
{% highlight rust %}
let mut valid_name = something;
valid_name = something_else;
{% endhighlight %}
This second version instructs Rust to create two memory locations for each `valid_name`. Only due to the Rust optimizer does the computer realize that it can reuse the same spot.
{% highlight rust %}
let valid_name = something;
let valid_name = something_else;
{% endhighlight %}

- When returning a reference to a `RefCell`, wrap the content with `Ref` which can be done through `Ref::map`.
{% highlight rust %}
fn get_associated_url(req: &net_traits::request::Request) -> Option<Ref<url::Url>> {
    // if into_inner() is used, req is no longer accessible
    let url_list = req.url_list.borrow();
    if url_list.len() > 0 {
        // .first() returns an Option, and therefor needs unwrap()
        Some(Ref::map(url_list, |urls| urls.first().unwrap()))
    } else {
        None
    }
}
{% endhighlight %}

## TODO:
- Headers:
    - Submit PR after final tests and squashing commits
- Response:
    - If Headers is accepted, start working on Response.
- Request:
    - Continue with constructor!

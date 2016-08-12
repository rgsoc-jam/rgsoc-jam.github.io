---
layout: post
title:  "Day 30: My Dearest Frenemy, Borrow Checker"
date:   2016-08-12
categories: [log]
comments: false
tags: [git, log, servo, rust]
authors: Jeena and Malisa
---

## Things we did:
- Response API
    - Wrapped `net_traits::response::Response`'s headers (`hyper::headers`) with `Rc` and `RefCell`.
    - Fought with the borrow checker the whole day. Implemented `clone` for `net_traits::response::Response` and dealt with side-effects of using internal `Rc` types... x_X
- Request API
    - Decided not to file a spec issue, but clarified the reasoning for the additional step in `request.rs` in the comments.
    - Made the code more readable, and removed unnecessary parts.
    - jdm gave me the permission to squash! Woohoo! Merge is near.

## Things we learned:
- Parentheses [are useful](https://is.gd/Q9SUOj)! Long story short, wrapping parentheses around `(*gadget1.owner)` applies the deref `*` to just `gadget1.owner`, which is just what I needed. :)

- Reflog is what git uses to keep track of updates to the tip of branches, including those that are invisible on git log! This acts as a great safety net. For example, if you want to undo git rebase, you can find the `HEAD` of pre-rebase, and `git reset --hard` to that `HEAD`.

- You cannot modify a field that is in a borrowed context. There are a few things going on in this code:
{% highlight rust %}
fn Referrer(&self) -> USVString {
    let r = self.request.borrow();
    let referrer = r.referer.borrow();
    USVString(match &*referrer {
        &Referer::NoReferer => String::from("no-referrer"),
        &Referer::Client => String::from("client"),
        &Referer::RefererUrl(ref u) => {
            let u_c = u.clone();
            u_c.into_string()
        }
    })
}
{% endhighlight %}
    - The reason there are `r` and `referrer` is that if it's written into one line (`let r_referrer = self.request.borrow().referer.borrow()`), it will throw a life time error. See [here](https://rgsoc-jam.github.io/articles/2016-08/cat-day).
    - In `match` if `referrer` does not have `&*`, it will throw a type mismatch error. This is because `referrer` is a `Ref<>` type, and it is trying to match against `Referer` enum.
    - So, you may want to dereference (`*referrer`) so that you can use `referrer` as a `Referer` enum type through deref coercions. However, that will be trying to move `referrer` out of borrowed context.
    - And therefore, you make it explicit that `referrer` is borrowed object, while dereferencing it: `&*referrer`
    - Similarly, in the last match arm, `u_c` is created because `u` is a `ref`. If you were to write `u.into_string()`, you will be trying to move `u` out of borrowed context.

## TODO:
- Response API:
    - Deal with current build errors (now the side-effects of wrapping headers with `Rc` and `RefCell` are appearing in places like fetch/methods.rs, uh oh)
    - And then modify `net_traits::request::Request` and `dom::headers` as well......
    - And then finally work on dom::Response! >:|
- Request API:
    - If merge happens, start working on making Headers iterable based on jdm's [PR](https://github.com/servo/servo/pull/12819).
- General:
    - Finish up writing blog post, intro to Rust's ownership.

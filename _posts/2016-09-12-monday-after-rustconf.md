---
layout: post
title:  "Day 49: The Wonder-debugging-land"
date:   2016-09-12
categories: [log]
comments: false
tags: [log, rust, servo]
authors: Jeena and Malisa
---
We went to RustConf last Saturday, and it was AWESOME.

![jammin the rustconf](/img/jammin-the-rustconf.jpg)

Malisa is sick :cry: and focused on getting better :tea:

## Things we did:
- Updating Headers
    - A [PR](https://github.com/servo/servo/pull/13004) that Jeena opened a while ago finally got merged after [fetch web platform test was updated](https://github.com/w3c/web-platform-tests/pull/3646).

- Promise in Fetch
    - On Friday, wrapping `Rc<Promise>` with `Trusted` didn't work. Over the weekend Josh pushed another commit to enable `Trusted<Promise>` and `TrustedPromise::root()` that will return a `Rc<Promise>`. On Sunday, I encountered two borrow check errors:
        - process_response requires `&mut self` as a parameter (not mut self). When I try to get the root of `TrustedPromise`, it throws an error saying "cannot move out of borrowed content”. [lines 122, 124, 136, and 138](https://gist.github.com/jeenalee/8f5ee01bb35188e1c3a18e366bd6967b#file-fetch-rs-L118-L141)
        - the `root()` of `TrustedPromise` requires self parameter. In line 101, with `let context = fetch_context.lock().unwrap();` which is type `MutexGuard`, which derefs to &T. When we try to access the `Rc<Promise>` via `context.fetch_promise.root()`, the compiler throws a [borrow error](https://gist.github.com/jeenalee/8f5ee01bb35188e1c3a18e366bd6967b#file-fetch-rs-L101-L103).
    - Today, I struggled a lot with the borrow checker, but now I have a compiling code! So I wrote [a short html page that uses fetch](https://gist.github.com/jeenalee/e68017aa24812a9349b1f3f8fb865b45) to run it on Servo! ([Based on MDN's example](https://github.com/mdn/fetch-examples/blob/gh-pages/fetch-request/index.html))
    - That helped me learn that Fetch isn't working :scream:. I started debugging (which means, me = stressed out) and learned a few things:
        - `metadata` that is used for `process_response` looks good. It's `Ok(_)` and has the fields that look not incorrect.
        - After promise is taken from FetchContext through `self.fetch_promise.take()`, no other line is called... WEIRD. WHY. Well, luckily, I was working at the Mozilla Office, and three(!) people helped me debug. Special thanks to @sanxiyn, @fitzgen, and @jimblandy.
    - So, after using the debugger, this is what we learned:
        - Here is the stack [backtrace](https://www.irccloud.com/pastebin/9kTP1yBn/).
        - Frame is older with higher frame number, i.e. `frame #6` is called before `frame #5`.
        - `frame #6` shows that `to_jsval` was called. This in turn calls `JS_WrapValue` in `frame #5`. This in turn calls `JSCompartment::wrap` in `frame #4`.
        - `JSCompartment::wrap` is a C++ code in SpiderMonkey, a JavaScript engine. `JSCompartment::wrap` has a parameter that is `this=&0x0`. `0x0` is a null pointer!!! We have a memory-unsafety here!!! Woohoo!

- Body
    - Read the spec and some more about Unicode encodings in order to understand the UTF-8 decoder. Wrote a little code. Progress was slow due to being sick today.

## Things we learned:
- When you write `.` after an object, it automatically derefs! For example, if I do `fetch_context.lock()`, I'm derefing `fetch_context` then applying the `lock()` method.
- assigning different types to the same binding name (via let statements) seems to be acceptable practice, at least in some contexts.
- `0x0` is the synonym to null pointer in C++! If your stack backtrace includes `0x0` that's probably not something you wanted :)
- When debugging Servo, you can use the `--debug` tag, i.e. `./mach run -d ~/src/fetch_example.html --debug`. Servo uses lldb debugger by default.
- You can set a breakpoint, for example, if you want the code to pause when it calls `rust_panic` function, you can write `b rust_panic` `<ENTER>` `run`.
- While you're at the breakpoint, (or maybe some other time too but I'm not too sure) you can type `bt` which will print all the backtrace! COOL.
- `Rc` and `Trusted` has to maintain a 1:1 relationship, and therefore, `Trusted` should not have a `&self` parameter because that could break that 1:1 constraint. In Servo's promise, `Rc` counts the references, and therefore `TrustedPromise` has to be connected to the one and only `Rc<Promise>`, because otherwise, the reference count will be incorrect.

## TODO:
- Promise in Fetch
    - Ask jdm about the null pointer!
- Body
    - continue with [UTF-8's decoder](https://encoding.spec.whatwg.org/#utf-8-decode)

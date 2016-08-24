---
layout: post
title:  "Day 37: Living the mug brownie life"
date:   2016-08-24
categories: [log]
comments: false
tags: [log]
authors: Jeena and Malisa
---

## Things we did:
- Miscellaneous
    - Made [mug brownies](https://encrypted.google.com/search?hl=en&q=mug%20brownie%20recipe), which were delish.

- Headers
    - [PR](https://github.com/servo/servo/pull/12998) is merged!
    - [PR](https://github.com/servo/servo/pull/13004) sparked some discussion… This might take a bit longer to resolve. Tried to implement header values to be stored as `Vec<Vec<u8>>` in which the inner vector is one header value. Not sure how this will mesh with hyper::header::Header existing methods. (Or, how do I separate the different header values? Will the comma have to be added as a separate vector?)
- Fetch
    - Started working on this, and encountered some ~issues~ challenges! See TODO.

- Response
  - Still dealing with wpt test errors. Fixed one (adding dummy argument to constructor so it takesthe right number of arguments), still dealing with a UTF-8 conversion error on one of the tests.

## Things we learned:
- if you want to import the latest changes in a file from a different branch to your current branch:
```
git checkout remote-name/branch /path/to/file
```

## TODO:
- Fetch
    - It looks like fetch requires `WindowOrWorkerGlobalScope` which is not implemented yet. Hear what Josh has to say, and do that!
- Response
  - Submit the PR once tests pass.
- Start trying to understand the work that would go into implementing the body APIs, working on top of jdm's Promise branch (Malisa)

---
layout: post
title:  "Day 11: Append is Still Almost There"
date:   2016-07-18
categories: [log]
comments: false
tags: [log, servo, rust]
authors: Jeena and Malisa
---

## Things we did:
- Addressed all the feedback from [PR#2](https://github.com/servo/servo/pull/12467). Tests appear to be passing. Fingers crossed!

## TODO:
- Modify [xmlhttprequest.rs](https://github.com/servo/servo/blob/master/components/script/dom/xmlhttprequest.rs#L412) to use our is_forbidden_header_name() function
- Come to a conclusion regarding the field-content production, i.e. [here](https://github.com/whatwg/fetch/issues/332).
- Write tests for our append method and associated helper functions
- Start working on [other Headers API methods](https://fetch.spec.whatwg.org/#headers), such as delete, get, set, has.

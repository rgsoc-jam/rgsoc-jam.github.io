---
layout: post
title:  "Day 46: Rusty things"
date:   2016-09-07
categories: [log]
comments: false
tags: [log, servo]
authors: Jeena and Malisa
---

## Things we did:
- Promise in Fetch
    - I feel like I didn't make much progress today. I've been looking at how XHR is implemented the whole day, and couldn't understand it very much :disappointed: What I get is that there needs to be an object (probably `FetchContext`) that will hold the intermediate Response, and communicate with Promise to get the status of fetch. Hopefully tomorrow will be different!
- Body
    - Started to write the extract-body function until I realized it's already been written in XHR.
    - Moved onto more of the Body logic. Not sure how ReadableStream will be dealt with. I feel like a lot of what I'm doing will cross tracks with what Jeena's doing. We'll see...!

## Things we learned:
- We went to the monthly Rust meetup today. We learned about some [patterns](https://github.com/nrc/patterns) we should and shouldn't do, a shout-out to [clippy](https://github.com/Manishearth/rust-clippy), and a [C to Rust converter](https://github.com/jameysharp/corrode) (wow!). We saw a lot of the Rust community in person (they flew in from around the world for the upcoming RustConf this weekend), so it was pretty exciting!

## TODO:
- Promise in Fetch
    - make FetchContext struct
    - Impl FetchResponseListener for FetchContext (may require helper functions)
    - resolve/reject promise in fetch
- Body
    - Continue with Body logic until I can't no more! (And then ask jdm :P)

---
layout: post
title:  "Day 59: D-4 "
date:   2016-09-26
categories: [log]
comments: false
tags: [log, git]
authors: Jeena and Malisa
---

## Things we did:
- Body
    - Spent the morning (!!) rebasing Body on top of master (did it the hard way using rebase the first time, until Jeena suggested I just reset and cherry-pick my commits on top...the latter way had only a few merge conflicts as opposed to a LOT). And a little rewriting to get things to compile. Still need to implement the BodyTrait for request.rs. More tests are passing now!! Yay :)
- Fetch
    - Hmm, homu tests kept failing. Web platform tests related to `cors/` and `redirect/` seemed to fail intermittently, so we decided to skip those tests for now.
- Package Data Algorithm
    - The parser for body when MIMEType is "multipart/form-data" is not clearly defined, so I decided to skip it for now.
- General
    - We started writing our end-of-summer blog post. So sad!

## Things we learned:
- `git cherry-pick` is sometimes easier than `git rebase`
- `git clean -f -d` gets rid of untracked files and directories. I used this today right before a `git reset`.

## TODO:
- Body
    - The JSON function still does not work. getting error: `WebIDL.WebIDLError: error: Unresolved type '<unresolved scope>::JSON'`
- Test Curation
    - Go through the new tests, and categorize them.

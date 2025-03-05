---
title: "Day #24"
description: "What is DerivedData?"
slug: "swift-daily-24"
date: 2021-09-09 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "derived data"
links:
  - title: "What's inside the Derived Data folder?"
    description: "Deleting derived data - a well know trick that comes in handy every time Xcode behaves strangely for no obvious reason. I still clearly remember when my senior told me about this basic iOS dev trick for the first time."
    website: "https://vojtastavik.com/2018/09/02/what-is-inside-derived-data-xcode/"
    image: ""
weight: 1
---

Derived data is stored at /Users/YourNameHere/Library/Developer/Xcode/DerivedData

At a basic level, it will cache build information for your projects, but let’s see what it actually stores.

- Precompiled module files. These files are an abstraction to reading in headers every time you import something in code. These files will be under a folder with a hash as a name. The hash takes in clang arguments as input.
- Index folder: You may have seen an indicator saying Indexing in progress... in Xcode. Basically, indexing is creating a quick way to search though your project. Xcode manages searching and find/replace stuff very nicely.
- Logs: Just a history of builds/testbuilds etc…
- Builds: The actual builds are saved. If you don’t change your code between runs, Xcode will just use the last stored build.
- Intermediates: Other files that need to be build for the project. These normally include libraries and frameworks. The great part about this section is that many of the files here don’t get modified too much, so the cache is very pure (is that a legit term to describe caches? Idk).

If you’ve ever had weird problems with xcode, you’re probably familiar with the delete derived data trick. I don’t know why problems arise here, or why deleting derived data works, but I hypothesize that it has something to do with cache invalidation bc that kind of stuff gets extremely hard at the low level.

Here’s a quick tip for all the avid Xcode users out there: Navigate to DerivedData and create an alias. Put that alias in your desktop folder. Tada! You now have a less annoying way of accessing DerivedData when you need to.

*Information for this post was sourced from the article linked below*

*Originally published 09/09/2021 https://pittcsc.org/, republished 09/09/2022.*

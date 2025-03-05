---
title: "Day #51"
description: "Objc Bridging"
slug: "swift-daily-51"
date: 2021-10-06 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "obj-c"
    - "bridging"
#links:
#https://swiftdoc.org/v2.0/type/array/
#https://developer.apple.com/documentation/swift/set
weight: 1
---

Bridging between data structures (set, array, dict) in swift and objc is usually O(1) time space complexity. If elements in these data structures are not classes or objc protocols or bridgeable to a foundation type they will be lazily converted on call, which is O(n). So…. do your research - some stuff is toll free, but some stuff is not.

*Originally published 10/06/2021 https://pittcsc.org/, republished 09/16/2022.*

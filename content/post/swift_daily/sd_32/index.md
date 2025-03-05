---
title: "Day #32"
description: "Codable (Part 2 of 4)"
slug: "swift-daily-32"
date: 2021-09-17 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "codable"
#links:
weight: 1
---

If you just have a 1:1 conversion like snake_case->camelCase, you do not need to do what was described in day #31, instead you can use built in decoding strategies.

```swift
let decoder = JSONDecoder()
decoder.keyDecodingStrategy = .convertFromSnakeCase
```

There are options for DefaultKeys, SnakeCase, and Custom. This technique comes with a performance cost, but is great for prototyping.

*Originally published 09/17/2021 https://pittcsc.org/, republished 09/09/2022.*

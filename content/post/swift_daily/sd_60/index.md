---
title: "Day #60"
description: "Implementation of Optionals"
slug: "swift-daily-60"
date: 2021-10-15 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "optionals"
#links:
weight: 1
---

This is the implementation behind optionals in swift:

```swift
enum Optional<T> {
  case some(T)
  case none
}
```

It is an algebraic data type. Swift has syntax to help make optionals more usable (if let, guard let, etc.)

*Originally published 10/15/2021 https://pittcsc.org/, republished 09/20/2022.*

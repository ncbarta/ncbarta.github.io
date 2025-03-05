---
title: "Day #40"
description: "Pattern Matching With Associated Values in Enums"
slug: "swift-daily-40"
date: 2021-09-25 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "associated values"
    - "pattern matching"
#links:
weight: 1
---

Yesterday’s feature gets a little bit more advanced.

You can actually do matching with it!

```swift
enum MyEnum {
    case multiple(_ firstValue: String, _ secondValue: Int)
}

if case let MyEnum.multiple(_, theSecondValue) = .multiple("anything", 10) {
    // True no matter what `firstValue` is
    print(theSecondValue)
}
```

**Code credit: Dustin @ Strega’s Gate**

*Originally published 09/25/2021 https://pittcsc.org/, republished 09/09/2022.*

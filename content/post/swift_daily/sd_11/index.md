---
title: "Day #11"
description: "Type Aliasing"
slug: "swift-daily-11"
date: 2021-04-13 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "type aliasing"
#links
#https://www.swiftbysundell.com/articles/the-power-of-type-aliases-in-swift/
weight: 1
---

Type aliasing is a way of giving a type a different name. It is useful for type-safe code organization, and cosmetics.

```swift
typealias Credit = Int

struct Course {
    let credits: Credit
}

```

*Originally published 04/13/2021 https://pittcsc.org/, republished 09/08/2022.*

---
title: "Day #39"
description: "Associated Values in Enums"
slug: "swift-daily-39"
date: 2021-09-24 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "associated values"
#links:
weight: 1
---

```swift
// Lets take an old example
enum Genre {
    case fiction
    case scifi
    case nonFiction
    case history
    case science
    case medical
    case other(name: String) //Associated value
}

// The defacto method for pulling out associated values invloves a switch statement

switch genre {
    case .fiction:
    //...
    case .other(let name): print(name)
}

// However there is actually another method to pull out just the associated value
if case let .other(name) == "poetry" {
    print(name)
}

//or 

if case .other(let name) == "poetry" {
    print(name
}
```

*Originally published 09/24/2021 https://pittcsc.org/, republished 09/09/2022.*

---
title: "Day #41"
description: "Logic Belongs Inside Enums Too"
slug: "swift-daily-41"
date: 2021-09-26 00:00:00+0000
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

Enum logic: You can clean up a lot of code by hiding logic in an enum.

```swift
enum Genre {
    case fiction
    case scifi
    case nonFiction
    case history
    case science
    case medical
    case other(name: String) //Associated value

    var isSciencey: Bool {
        switch self {
            case .scifi, .science, .medical: return true
            default: return false
        }
    }
}
//The code above lets us do this:
let isSciencey = someGenre.isSciencey

//Instead of this:
let isSciencey = someGenre == .scifi || someGenre == .science || someGenre == .medical
```

*Originally published 09/26/2021 https://pittcsc.org/, republished 09/09/2022.*

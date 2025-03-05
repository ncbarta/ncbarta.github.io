---
title: "Day #26"
description: "Where Clause"
slug: "swift-daily-26"
date: 2021-09-11 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "where clause"
#links:
weight: 1
---

Swift has “where” clauses that allow you to put logic in loop statements and extensions

```swift
let list = Array(0...100)

for x in list where x < 50 {
    print(x)
}

// For an example with extensions, see day #10!
```

*Originally published 09/11/2021 https://pittcsc.org/, republished 09/09/2022.*

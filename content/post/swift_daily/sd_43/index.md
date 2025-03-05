---
title: "Day #43"
description: "Rethrows"
slug: "swift-daily-43"
date: 2021-09-28 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "rethrows"
#links:
#https://www.avanderlee.com/swift/rethrows/
#https://www.hackingwithswift.com/example-code/language/how-to-use-the-rethrows-keyword
weight: 1
---

Rethows is a keyword to indicate that a function is wrapping around a throwing function.

```swift
func iThrow() throws -> Bool {}
func iDontThrow() -> Bool {}

func iWrap(t: (Void) -> throws Bool) rethrows {}
```

iWrap can wrap either of the functions. During compilation, Swift can tell if the wrapped function throws or not - which means it will not ask you to implement try/catch for a iDontThrow() parameter.

*Originally published 09/28/2021 https://pittcsc.org/, republished 09/16/2022.*

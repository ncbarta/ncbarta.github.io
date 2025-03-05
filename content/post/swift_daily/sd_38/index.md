---
title: "Day #38"
description: "Lazy Properties"
slug: "swift-daily-38"
date: 2021-09-23 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "lazy"
    - "autoclosure"
#links:
weight: 1
---

```swift
//Marking vars with the "lazy" keyword will make it so they are only initialized if called, and only initialized once.
lazy var dateFormatter = DateFormatter()

//One cool feature of Swift a lot of people don't realize is that constants work the same way!! The following object will only be initialized if/when it gets called. It's even thread-safe. Warning: it will stay in memory unless you manually manage it or it gets dereferenced. Be extra cautious if it is global.
static let someBigAsset = MegaClass()
```

## Other tips

> To add onto this, you can use the @autoclosure closure keyword instead of @escaping to give lazy-like tendencies to your closures. Auto closure means the closure won’t initialize or execute until it’s called, so it saves execution time. <br>
> — <cite>Josh Jaslow</cite>

*Originally published 09/23/2021 https://pittcsc.org/, republished 09/09/2022.*

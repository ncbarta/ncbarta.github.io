---
title: "Day #8"
description: "Enums are really powerful!"
slug: "swift-daily-8"
date: 2021-04-10 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "enum"
    - "enumeration"
#links
#https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html
weight: 1
---

Associated values: You can store custom values in an enum.

```swift
enum Genre {
    case fiction
    case scifi
    case nonFiction
    case history
    case science
    case medical
    case other(name: String) //<———
}
```

Raw values: You can store raw values in an enum. This can be used to wrap a reference type like a String (see below) in a value type (enum).

```swift
enum Routes: String {
    case home = “/home”
    case about = “/about”
    case library = “/library”
    case contact = “/contact”
}
let homePath: URL = URL(“www.you.com” + Routes.home.rawValue)
```

There is so much more (recursive enums, putting methods inside enums, unwrapping enums, ..)! Enums can be used for so much more than just “options”. One cool thing I’ve seen enums used for before is controlling a C state machine.

*Originally published 04/10/2021 https://pittcsc.org/, republished 09/08/2022.*

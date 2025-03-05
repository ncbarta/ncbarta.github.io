---
title: "Day #73"
description: "Metatypes (Part 1 of X)"
slug: "swift-daily-73"
date: 2022-09-15 00:00:01+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "metatype"
#links:
#https://medium.com/swiftcraft/introduction-to-swift-metatypes-21949842d7a
#https://swiftrocks.com/whats-type-and-self-swift-metatypes
weight: 1
---

A metatype is a type of a type. OK post done…..jk

Metatypes are used to access properties and methods (including initializers) belonging to a type - in contrast to an instance. Every time you use a static property or function, you are using a Metatype.

```swift
let whatsGoingOnHere: Int.Type = Int.self // Int.Type is a type, and Int.self is an instance
let a = SomeClass() // what’s actually happening is SomeClass.self.init()
```

They are helpful for generic code. In fact, Codable & UITableView have methods using parameters of X.Type.

To be continued…

*Originally published 09/15/2022 https://pittcsc.org/, republished 09/20/2022.*

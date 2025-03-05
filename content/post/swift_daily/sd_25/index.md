---
title: "Day #25"
description: "Linked Lists and Indirect Enums"
slug: "swift-daily-25"
date: 2021-09-10 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "linked list"
    - "indirect enum"
#links:
weight: 1
---

It is possible to make a linked list in 4 lines of code in Swift (but just because you can do something doesn’t mean you should)

```swift
indirect enum LinkedListNode<T> {
    case value(value: T)
    case next(value: T, next: LinkedListNode)
}

switch currentNode {
  case .value(let value): print(value)
  case .next(let value, let next): print(value); currentNode = next 
}
```

*Originally published 09/10/2021 https://pittcsc.org/, republished 09/09/2022.*

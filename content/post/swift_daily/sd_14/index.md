---
title: "Day #14"
description: "Variatic parameters"
slug: "swift-daily-14"
date: 2021-04-16 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "variatic parameters"
    - "functions"
    - "methods"
#links
#https://www.swiftbysundell.com/tips/the-power-of-variadic-parameters/
weight: 1
---

Swift has variadic parameters. This allows you to put multiple things into a function without having to use an array. It is notated with the range syntax “…”

```swift
//EXAMPLE FROM https://www.swiftbysundell.com/tips/the-power-of-variadic-parameters/
// When using a variadic parameter, any number of arguments can
// be passed, and the compiler will automatically organize them
// into an array.
func send(_ message: Message, attaching attachments: Attachment...) {
    ...
}

// Passing no variadic arguments:
send(message)

// Passing either a single, or multiple variadic arguments:
send(message, attaching: image)
send(message, attaching: image, document)
```

You always have the option of using an array if you want, like:

```swift
send(message, attaching: […])
```

*Originally published 04/16/2021 https://pittcsc.org/, republished 09/08/2022.*

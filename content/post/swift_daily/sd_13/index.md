---
title: "Day #13"
description: "Guard statement"
slug: "swift-daily-13"
date: 2021-04-15 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "guard"
    - "conditionals"
    - "branching"
#links
weight: 1
---
A *guard* statement is basically a reverse *if* statement

```swift
guard textField.text! != “” else { exit(1) } //If the condition is true, the program will continue. Kind of like a safe “assert()”

//Guard statements can also be used to unwrap optionals
guard let entry = someEntryField.entry else { presentWarning(“You have not entered anything”); return }
```

# Why do these even exist?

First of all, they make your code prettier. They can flatten some code structures like *pyramids of validation*. It takes less effort to read “guard” and know what it means instead of “if !() {}”. Secondly, it introduces a method of unwrapping an optional and placing it in the active scope, instead of inside a body like an “if let” statement.

*Originally published 04/15/2021 https://pittcsc.org/, republished 09/08/2022.*

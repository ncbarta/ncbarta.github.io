---
title: "Day #10"
description: "Swift Extensions"
slug: "swift-daily-10"
date: 2021-04-12 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "extension"
#links
#https://www.swiftbysundell.com/articles/the-power-of-extensions-in-swift/
weight: 1
---

Swift extensions are probably one of the most powerful features of the language.

You can place extra code in extensions and it will be as if the code was in the entity itself.

In short: “Extension methods are a special kind of static method, but they are called as if they were instance methods on the extended type.”


```swift
class Army {
    func giveCommand(command: String) -> CommandID {}
}

extension Army {
    func rescindCommand(id: CommandID) -> Bool {} //This code is as if it is in class Army
}

//All arrays with type Army will now have a “deploy” functionality. This feature can be used in real scenarios like sorting ect…
extension Array where Element: Army {
    func deployAll() {}
}
```

*Originally published 04/12/2021 https://pittcsc.org/, republished 09/08/2022.*

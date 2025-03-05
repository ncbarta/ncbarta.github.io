---
title: "Day #4"
description: "Swift Optionals Crash Course"
slug: "swift-daily-4"
date: 2021-04-06 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "Optionals"
weight: 1
---

Optionals are notated by a “?” postfix. Some types are optional by default. If a type is optional, it either has a value, or is nil. There are a lot of things that are optionals, such as images and text fields. Optionals allow for more logical API’s

```swift
var age: Int? //Custom optional. Since it is optional, it does not need to be instantiated inside a class. It can be assigned to later.
let image: UIImage = UIImage(named: “profilePic”) //Type will be optional by default
let textField: UITextField = UITextField() //Type will be optional by default

//Optional values have to be “un-wrapped” to be used, because something can’t both have a value and be nil.
//There are multiple ways to un-wrap an optional

////SAFE METHODS:

if let text = textField.text {
    //“text” will be accessible inside here if it exists
}

guard let text = textField.text else { return } //text will be available following declaration

let text = textField.text ?? “” //If textField is nil, “” will be given as a default value

////UNSAFE METHODS:
let text = textField.text! //This will crash if the optional is nil. You should only use this if you know the value will never be nil
```

*Originally published 04/06/2021 https://pittcsc.org/, republished 09/08/2022.*

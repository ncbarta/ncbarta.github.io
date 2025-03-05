---
title: "Day #5"
description: "What is the protocol-delegate communication pattern?"
slug: "swift-daily-5"
date: 2021-04-07 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "Protocol Delegate"
    - "Communication"
weight: 1
---

The Protocol-delegate pattern is a method of subscribing methods to an event.

```swift
protocol ButtonPressedDelegate: AnyObject {
    func methodToBeImplemented()
}

class ReceivingClass: UIViewController, ButtonPressedDelegate {
    
    func methodToBeImplemented() { //Conform to protocol
        print(“Button pressed”)
    }

}

class SendingClass: UIViewController {
    weak var delegate: ButtonPressedDelegate? //Create field for reference. Use “weak var” to avoid retain cycle.
    
    @IBAction func send(_ sender: Any) {
        delegate.methodToBeImplemented() //Call method
    }
}

let receivingC = ReceivingClass()
let sendingC = SendingClass()
sendingC.delegate = receivingC.self //Pass the reference. Normally you would not do it like this, but this is the concept.

//Better places to assign a reference:
//-From inside cellForRowAt()
//-In a segue
//-As you instantiate sending class from receiving class

//Common errors:
//-Protocols are one-to-one. If you are trying to subscribe multiple receivers, you will need to implement a multicast delegate. Dm for code snippet.
//-Forgetting to assign self to delegate field in sending class.
//-Issues with “weak self”, make sure to conform the protocol to AnyObject

//For more code ideas, and a explanation an why we use “weak var”: https://medium.com/macoclock/delegate-retain-cycle-in-swift-4d9c813d0544
```

*Originally published 04/07/2021 https://pittcsc.org/, republished 09/08/2022.*

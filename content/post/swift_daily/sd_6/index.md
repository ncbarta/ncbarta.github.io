---
title: "Day #6"
description: "What is the protocol-delegate communication pattern?"
slug: "swift-daily-6"
date: 2021-04-08 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "@IBAction"
    - "@IBOutlet"
#links
#https://janlcodesiboutlets-and-ibactions-in-the-cocoa-touch-framework-dfcc9d6c77b2/
#https://nshipster.com/ibaction-iboutlet-iboutletcollection/
#https://www.swiftbysundell.com/articles/property-wrappers-in-swift/
#https://medium.com/the-traveled-ios-developers-guide/swift-attributes-936f3426d5db
#https://docs.swift.org/swift-book/documentation/the-swift-programming-language/attributes/
weight: 1
---

@IBAction & @IBOutlet: These are remnants of Obj-c, and pre-macOS10.3. Before Xcode existed, there was something called Project Builder. To create views for Project Builder, you had to use a separate application called Interface Builder, which made .nib files & the object graph. @IBOutlet and @IBAction were used as keywords to expose Project Builder code to Interface builder. Note that the “IB” in these keywords stands for Interface Builder.

These keywords do not actually have any meaning in a modern context, especially @IBAction, since any object from the Interface Builder (now included in Xcode) can be attached to any function matching this pattern: name(_ sender: ) -> Void.

@IBOutlet keyword however is still needed to link properties in the IB and code.

Property wrappers: Putting @propertywrapper before a class lets you create a type that has some functionality ever time it is changed. For example, you could make “@propertywrapper class Flipped{}”, and every data field with “@Flipped” before it would have it’s value flipped upon assignment. @Flipped var name: String name = “Nathan” print(name) //prints “nahtaN” Just like everything else in Swift, these can get insanely powerful.

Objc: Adding @objc will expose your Swift code to the Objective-C runtime. This is needed for some functionalities like UIGestureRecognizer, and other things still rooted in Obj-c.

Attributes: There is a whole class of Swift functionality based off of something called attributes. @objc is one of these attributes, as well as property wrappers. There are tons of these that perform all kinds of black magic, so I will just leave you with articles at the end of this post.

*Originally published 04/08/2021 https://pittcsc.org/, republished 09/08/2022.*

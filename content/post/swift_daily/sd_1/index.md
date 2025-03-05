---
title: "Day #1"
description: "What is the difference between Foundation, Darwin, and CoreFoundation?"
slug: "swift-daily-1"
date: 2021-04-03 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "Foundation"
    - "Core Foundation"
    - "Darwin"
links:
  - title: "swift-corelibs-foundation"
    description: "The Foundation Project, providing core utilities, internationalization, and OS independence"
    website: "https://github.com/apple/swift-corelibs-foundation/blob/main/Docs/Design.md"
    image: "https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png"
  - title: "Apple/Documentation/Foundation"
    description: "Access essential data types, collections, and operating-system services to define the base layer of functionality for your app."
    website: "https://developer.apple.com/documentation/foundation"
    image: "https://developer.apple.com/apple-logo.svg"
  - title: "Apple/Documentation/CoreFoundation"
    description: "Access low-level functions, primitive data types, and various collection types that are bridged seamlessly with the Foundation framework."
    website: "https://developer.apple.com/documentation/corefoundation"
    image: "https://developer.apple.com/apple-logo.svg"
weight: 1
---

The Foundation framework is an Obj-C framework part of Swift’s core libraries. It is the root of all NSObject types. Foundation is closed source.

The Core Foundation (CF) framework is a lower level C implemented library part of Swift’s core libraries. It is the root of all CF types. CF objects must have their memory managed manually. CF does not need a Obj-C runtime. CF is open source.

The difference between these two frameworks is mostly that CF has a very limited Object model (it is C based after all). On the backend, foundation and CF can convert between each other toll-free.

Darwin is a bridge to commonly used C functions. It is a superset of CoreFoundation & Foundation. Here is an example of how it might be used with compiler directives for system specific code:

```swift
#if os(macOS) || os(iOS)
import Darwin
#elseif os(Linux)
import Glibc
#endif
```

There is also Swift standard library, which provides basic types like Strings.

*Originally published 04/03/2021 https://pittcsc.org/, republished 09/08/2022.*

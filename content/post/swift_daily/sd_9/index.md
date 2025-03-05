---
title: "Day #9"
description: "The 5 access control keywords"
slug: "swift-daily-9"
date: 2021-04-11 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "access control"
    - "keywords"
#links
#https://docs.swift.org/swift-book/documentation/the-swift-programming-language/accesscontrol/
weight: 1
---

```swift
open class Book { //An “open” class allows subclassing within a context outside of the defining module
    private var name: String //Restricts access to enclosing declaration. Extensions in same class file will be able to access.
    public var isbn: UUID //Does not restrict access.
    fileprivate var genre: String //Restricts access outside of the defining *file*. Classes within the same file will be able to access.
    internal var length: Int //Restrict access outside of the defining *module*.
}
```

Protected does not exist because:
- It is ambiguous as to whether an extension should be able to access it
- Subclass methods could expose it anyway

All vars/classes/types/entities have a access level of internal by default.

Modifiers:
- If you give something the @testable attribute, it will be accessible by the testing classes, but maintain status as internal/private otherwise.
- You can define access control to an entire class/struct. This will also carry through for all it’s members (properties, methods, initializers, and subscripts)
- If you create a tuple out of two differently access controlled types, it will assume the most restrictive one.
- A function will be as restrictive as it’s parameters or return types are, unless you specify.
- Enum cases cannot have different levels of access, as well as their raw and associated values
- Type aliases can only have the same access level, or a more restrictive one.* this is an oversimplification

*Originally published 04/11/2021 https://pittcsc.org/, republished 09/08/2022.*

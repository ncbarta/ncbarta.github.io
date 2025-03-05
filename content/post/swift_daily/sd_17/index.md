---
title: "Day #17"
description: "Structs vs Classes (Part 2 of 2)"
slug: "swift-daily-17"
date: 2021-04-19 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "structs"
    - "classes"
#links
weight: 1
---

Structs, as long as they are comprised of less than or equal to 3 words, who’s words are primitive or first-class, are generally performant, as long as they do not implement a protocol. This is because they reside in the stack instead of the heap, have no references (although a struct requires reference counting if its properties require it), and are statically managed. To make data fields first class, you can abstract them with other types, such as an enum which implements String, or Hashable. Swift arrays can also store structs directly, instead of using references - which can be EXTREMELY useful (consider an array of type “points” comprising a mesh/graph).

Classes are generally performant too, as long as you keep the references down, and try to make them statically called by declaring them “final”. Marking data fields as “final” is also very performant, as it eliminates compiler-side getter setter override checks. Marking functions as private can have the same effect. Giving the compiler more information, such as the module hierarchy (Enable “Whole Module Optimization”), will lead to automatic optimization, because it will check classes for sub-classes and such. This is one of the reasons that Swift is faster than obj-c.

*Originally published 04/19/2021 https://pittcsc.org/, republished 09/08/2022.*

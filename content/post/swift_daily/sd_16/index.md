---
title: "Day #16"
description: "Structs vs Classes (Part 1 of 2)"
slug: "swift-daily-16"
date: 2021-04-18 00:00:00+0000
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

## Classes

Swift classes are reference types. This means if you assign a class to a field, you are passing a reference around. In order to copy a class, you will have to make a shallow or deep copy.

## Structs

Swift structs are value types. This means if you are passing a copy around. Every time you move a struct, you create a new copy of the struct.

## Why?

First thing to note is that Structs are not unique to Swift. They are present in many languages, such as C, C#, C++, golang. Some languages implement structs as derivatives of other data structures, and some langagues do not have them at all (java, python). Structs are generally more performant if used right - which is a distinct advantage. However, the biggest advantage is probably just the differences in copying versus referencing. Structs help you move your code towards a more data-oriented approach.

*Originally published 04/18/2021 https://pittcsc.org/, republished 09/08/2022.*

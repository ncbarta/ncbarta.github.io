---
title: "Day #20"
description: "SPM (Part 1 of 3)"
slug: "swift-daily-20"
date: 2021-04-22 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "spm"
    - "swift package manager"
#links
#https://www.swift.org/documentation/package-manager/
weight: 1
---

Ok, I’ve mentioned SwiftPM or SPM multiple times now - but what is it?

SwiftPM is a built-in dependency manager for Swift code. SwiftPM allows users to create, distribute, download, and link modules. Modules can either be libraries, or executables.

Here is the basic file structure of a module:

```
ModuleName
├── Sources
│   └── ModuleName
│       ├── File1.swift
│       ├── File2.swift
└── Package.swift
```

The Package.swift file is the most important part, as it organizes the module.

*Originally published 04/22/2021 https://pittcsc.org/, republished 09/09/2022.*

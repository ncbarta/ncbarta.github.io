---
title: "Day #21"
description: "SPM (Part 2 of 3)"
slug: "swift-daily-21"
date: 2021-04-23 00:00:00+0000
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

Here is what a package file looks like. You may note that it looks similar to JSON.

```swift
// swift-tools-version:5.3      //<- This comment is necessary, it specifies tool version
import PackageDescription

let package = Package(
    name: "MyLibrary",
    platforms: [
        .macOS(.v10_15),
    ],
    products: [
        .library(name: "MyLibrary", targets: ["MyLibrary"]) //Here is where you can define products. They can be libraries or executables
    ],
    dependencies: [
        .package(name: “Utility”, url: "https://github.com/user/repo.git", from: "1.0.0") //Import the latest version >1.0.0. Alternatively, you can use .exact(“1.0.0”) to get an exact version. There are also ranges and such. If there are multiple packages, SPM will try to get the most up to date combination where all dependencies work with eachother.
    ],
    targets: [
        .target(name: "MyLibrary", dependencies: ["Utility"]), //Targets, basically what you would run.
        .testTarget(name: "MyLibraryTests", dependencies: ["MyLibrary"])
    ]
)
//There are way more features you can take advantage of.
```

*Originally published 04/23/2021 https://pittcsc.org/, republished 09/09/2022.*

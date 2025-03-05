---
title: "Day #7"
description: "Swift is interoperable with Obj-C and C."
slug: "swift-daily-7"
date: 2021-04-09 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "interoperability"
    - "interop"
    - "binding"
    - "SwiftPM"
    - "modulemap"
#links
#https://rderik.com/blog/understanding-objective-c-and-swift-interoperability/
#https://theswiftdev.com/how-to-call-c-code-from-swift/
weight: 1
---

With a little (lot) of finagling, you can run C libraries from Swift, which opens the doors to higher performance and graphical/musical/computational applications.

The basic structure for importing a C library in Swift might look like this:

Compiled C library on system in users/lib or wherever it is default -> Make a module -> Import as system library with SwiftPM (SwiftPackageManager) into that module -> Make sure linker is working correctly -> Create modulemap file and Bridging header file (also sometimes called a shim) -> Configure these files -> Import this module into your project using SwiftPM.

It is very difficult since SwiftPM does not tell you what you are doing wrong, and there is not a lot of good help online.

*Originally published 04/09/2021 https://pittcsc.org/, republished 09/08/2022.*

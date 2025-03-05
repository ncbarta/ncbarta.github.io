---
title: "Day #30"
description: "How Do You Measure The Speed of Swift Code?"
slug: "swift-daily-30"
date: 2021-09-15 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "benchmarks"
#links:
#https://swiftrocks.com/benchmarking-swift-code-properly-with-attabench
weight: 1
---

Well, first things first, compile it. Putting your code in a playground/REPL is not going to give you accurate results. The best way to test your code is with testing frameworks. You can test sections of pure swift easily with attabench https://swiftrocks.com/benchmarking-swift-code-properly-with-attabench. Xcode of course comes with it’s own profiling tools (called instruments) for testing things such as launchtime, time, leaks, memory usage, battery usage, network/file usage, and much more - which is applicable to full scale application testing.

*Originally published 09/15/2021 https://pittcsc.org/, republished 09/09/2022.*

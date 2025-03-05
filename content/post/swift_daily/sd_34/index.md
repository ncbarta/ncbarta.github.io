---
title: "Day #34"
description: "Codable (Part 4 of 4)"
slug: "swift-daily-34"
date: 2021-09-19 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "codable"
#links:
weight: 1
---

## Working with codable dates

There are many ways to represent a date in CS. With codable, you can code and convert date representations to match the Date() type in swift.

```swift
//Decoding example. Convert an ISO8601 to Date()
let decoder = JSONDecoder()
decoder.dateDecodingStrategy = .iso8601

//Custom: You can also decode from a custom date format using DateFormatter().
decoder.dateDecodingStrategy = .formatted(someCustomDateFormatter)

//You can also decode with a closure
decoder.dateDecodingStrategy = .custom { decoder in
  //...
  return ...
}
```

*Originally published 09/19/2021 https://pittcsc.org/, republished 09/09/2022.*

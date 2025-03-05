---
title: "Day #31"
description: "Codable (Part 1 of 4)"
slug: "swift-daily-31"
date: 2021-09-16 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "codable"
#links:
weight: 1
---

Data coming from (or going to) an API is not always organized/standardized. For instance, the json keys could have different naming schemes. Consider the case below:

```json
{
    first_name: ""
    MiddleName: "",
    lastName: "",
}
```

So how does this get coded? By using a feature called codingkeys. Simply create an enum inside the object you are decoding to as following:

```swift
struct Name: Codable {
  let firstName: String
  let middleName: String
  let lastName: String
  enum CodingKeys: String, CodingKey {
    case firstName = "first_name"
    case middleName = "MiddleName"
    case lastName = "lastName"
  }
}
```

This codingkeys enum will allow the codable object to map to the json keys.

*Originally published 09/16/2021 https://pittcsc.org/, republished 09/09/2022.*

---
title: "Day #15"
description: "Computed Properties"
slug: "swift-daily-15"
date: 2021-04-17 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "computed properties"
#links
weight: 1
---

Computed properties are variables that compute when they are called

```swift
//Example
var tempFahrenheit: Int = 90
let tempCelsius: Int { return (32 * tempFahrenheit − 32) × 5/9 }
```

They are useful for disposable resources.

```swift
//Here is an example that i’ve seen in the wild. It just converts ints into other types. 
extension Int {     
    public var g: CGFloat {         return CGFloat(self)     }     
    public var d: Double {         return Double(self)     }     
    public var f: Float {         return Float(self)     }     
    public var b: Int8 {         return Int8(self)     }     
    public var ub: UInt8 {         return UInt8(self)     }    
    public var s: Int16 {         return Int16(self)     }    
    public var us: UInt16 {         return UInt16(self)     }     
    public var i: Int32 {         return Int32(self)     }     
    public var ui: UInt32 {         return UInt32(self)     }  
    public var ul: UInt {         return UInt(self)     }     
    public var ll: Int64 {         return Int64(self)     }     
    public var ull: UInt64 {        return UInt64(self)     } 
}
```

Computed properties do not have to be used for code organization. They are also great for dealing with values that are constantly changing.

*Originally published 04/17/2021 https://pittcsc.org/, republished 09/08/2022.*

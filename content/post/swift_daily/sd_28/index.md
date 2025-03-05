---
title: "Day #28"
description: "Using HTTP in iOS Apps"
slug: "swift-daily-28"
date: 2021-09-13 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "http"
#links:
#https://medium.com/collaborne-engineering/self-signed-certificates-in-ios-apps-ff489bf8b96e https://developer.apple.com/library/archive/qa/qa1948/_index.html
weight: 1
---

If your API is HTTP only, there is nothing you have to do. However, if you are using a self-signed certificate for HTTPS (testing purposes of course), there are extra things to do. iOS apps will not trust self-signed certs.

## Method 1: Force Trust (not recommended)

1. Add key “Allow Arbitrary Loads : YES” to “App Transport Security Settings” in info.plist
2. Wherever you are making the https calls, conform the class to URLSessionDelegate and add

## Method 2: Install the cert to the device (recommended)

You can simply transfer the cert file to the device, and then configure it in settings. https://medium.com/collaborne-engineering/self-signed-certificates-in-ios-apps-ff489bf8b96e https://developer.apple.com/library/archive/qa/qa1948/_index.html

## Notes

If you leave test code from Method 1 in your app, it is likely that your app will not be accepted bc it’s a security flaw. Using compiler directives to distinguish between test and build versions could be useful, but you still might get rejected. There are more complicated setups out there, but you won’t probably use them unless you work at a big company.

*Originally published 09/13/2021 https://pittcsc.org/, republished 09/09/2022.*

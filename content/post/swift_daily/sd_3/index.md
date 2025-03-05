---
title: "Day #3"
description: "What are Swift’s web development prospects?"
slug: "swift-daily-3"
date: 2021-04-05 00:00:00+0000
#image:
categories:
    - "Swift Daily"
#tags:
keywords:
    - "Server Side Swift"
weight: 1
---

Swift is a great choice for web development due to the following features:
- Speed. Swift’s loops are lightning fast. Loops are very important for web-backends
- Shared models. You can share a single data model file between your web app and mobile app (EX: DefaultUser.swift). This can cut down on development costs and time MASSIVELY. It’s also super clean and…
- Expressive. Swift is super expressive. This is always an advantage.

Swift also has some disadvantages when it comes to web development:
- Lack of unified async functionality. Swift does not have default async functionality yet, although it is in the making. Currently, there are 3rd party solutions for promises and await. The “default” way of doing async in Swift is using closures as completion handlers. Swift’s async features when they arrive will be similar to GOlang’s.
- Lack of information and adoption

Frameworks:
- Vapor: The most adopted Swift web framework. It is very fast and focuses on modular design. It is capable of making very complex apps. It is slightly bulky compared to other options. There is a good amount of information on it. I recommend https://theswiftdev.com/practical-server-side-swift-using-vapor-4-book/ by Tibor Bödecs.
- Perfect: This is the fastest web framework in the world*. It is very lightweight and does not have a lot of information on how to use. However, it should be pretty intuitive to use for people who are experienced. It is a refined framework, however I do not know if it will continue to be maintained.
- Kitura: Mostly discontinued. It was supported by Microsoft for awhile, but lost the battle against Vapor. Kitura is still usable. It has a low memory footprint, good documentation, and still fulfills it’s purpose of working well on the cloud.

*tied with pretty much every other advanced web framework. It’s all really subjective.

*Originally published 04/05/2021 https://pittcsc.org/, republished 09/08/2022.*

---
title: "HackNC 2022"
description: "My hacknc2022 project"
slug: "hacknc2022"
date: 2022-11-21 00:00:00+0000
#image:
tags:
    - "Crypto"
    - "Go"
    - "gRPC"
    - "Trading"
    - "Algorithms"
keywords:
    - "golang"
weight: 1
---

# HACKNC2022

A few weeks ago I had the chance to participate in HackNC 2022. I chose the financial track.

## What I built

{{< youtube ZX0DjC1lMqA >}}

Tempest is a manager for trading algorithms. Basically, it is an abstraction between the systems for placing orders on the exchange, and your trading algorithms. I made this because when I used to run trading bots, it was very annoying to manage them. With Tempest you can write trading algorithms in whatever language you want & not worry about how their signals get turned into trades. In the future it would be awesome for Tempest to also manage deployment.

Unfortunately, I was not able to finish all that I wanted, but I learned a ton along the way, such as: gRPC, interprocess communication, protobuf.

Narrowly avoided FTX going out of business and ruining the Exchange~Tempest part of my project.
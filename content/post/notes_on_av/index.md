---
title: "Notes on AVVideo Compression"
description: ""
slug: "notes-avvideo-compression"
date: 2023-01-09 00:00:00+0000
#image:
tags:
    - "Swift"
    - "MacOS"
    - "iOS"
    - "Video"
    - "Compression"
    - "Documentation"
keywords:
    - "AVVideo"
weight: 1
---

*this post is a work in progress (~50% done) & may not be completely factual*

# Notes on AVVideo Compression

Recently I was tasked with fixing and adding new features to a video pipeline. Our app was supposed to record the user and save a compressed file to remote storage, however, our video files were getting corrupted. This post has some helpful information about Apple’s video encoding APIs. Not all information is 100% tested or factual - there is some speculation & I am not super knowledgable about this topic.

## Compression Considerations

Modern compression algorithms take into account spacial (intra-) and temporal (inter-) compression. Spacial compression is similar to text compression, it tries to compress pixels within a frame into the smallest form factor. Temporal compression stores the difference between frames, which means areas of video that don’t change much get stored much more compactly.

Two of the most common codecs are H264 and H265 (HEVC). They can both technically encode lossless, but the majority of users, including me, choose lossy settings. HEVC can store the same quality video in about 50% of the space as H264, however there are compatibility issues in browsers, so you should evaluate who’s going to be watching your videos, and what capabilities exist. I chose to offer configurations for both codecs. Our videos are stored in mp4 containers with no audio.

## Compression terms

### Bit Rate

Bit rate is the number of bits required to represent one second of video. In our case, one of our configurations was for HD (1080x720) @ 60fps, with a pixel format of 32_BGRA. This means, uncompressed, our video takes about 1080x720x32x60 = 1,492,992,000 (1492.992 mbit/s, ~1.5 Gbit/s). Since the average upload speed is currently ~23 Mbps (https://www.speedtest.net/global-index/united-states#fixed), it would take ~65sec to send 1 second of video & a single 26 second video would cost almost 5GB of storage.

For this reason, we select a bit rate far lower than what’s needed for uncompressed video.

Bit Rate = # of pixels * FPS * BPP

### Bits per pixel (BPP)

The number of bits to encode a pixel. 3 is considered “visually lossless”, which is a far cry from the 32 we were using in the above example. Selecting a number between 0.05 and 0.1 will have very noticeable differences. Numbers between 0.1 and 3 will usually have diminishing returns.

Multiplying the bit rate by 0.131072 can give you a loose estimate for the MAX number of MB/s your video will consume.

### Keyframes (I-Frames)

There are multiple types of frames in a video. Keyframes are just a picture. If you were to have all keyframes, the video would only use spacial compression.

### P-Frames and B-Frames

These frames are what makes temporal compression work. They represent the differences between frames & are placed between two keyframes.

### Group of Pictures (GOP)

Distance between two keyframes. I-Frames sandwich a group of P-Frames and B-Frames.

## AVVideoCompressionPropertiesKey

This section has descriptions of what the basic AVVideoCompressionPropertiesKey’s do, as well as some VideoToolbox keys.

In my understanding, these settings are often seen as a “suggestion” to the encoder & may not always be followed as expected.

| Name | Description | Considerations | Notes |
|---|---|---|---|
| AVVideoAverageBitRateKey | The average bit rate that the encoder will shoot for. | If this value is set too low & the encoder has no other options to degrade video quality to fit the bitrate target, the encoder will *fail* and spit out a corrupt file. Give the encoder options, such as droppable frames, wider max GOP, wider QP (image quality) range. If the encoder is not struggling to fit into the bit rate, it will take up it’s space & return the highest quality video it can. | Documentation falsely states that this property only applies to H264. |
| AVVideoExpectedSourceFrameRateKey | The frame rate of the input device connected to the AVCaptureSession. | | AVCaptureSession has basic presets available statically within code, however, there are additional device presets available during runtime (AVCaptureDevice.Format). |
| AVVideoMaxKeyFrameIntervalKey | Keyframe interval, aka GOP. 1 = 1th = every frame is a keyframe, 2 = 2nd = every other frame is a keyframe, 3 = 3rd = every third frame is a keyframe, etc… | Having all keyframes restricts the encoder to spacial compression only. This is MAX key frame interval. If you have extra space in the bitrate, the encoder will pick a smaller GOP (if a large GOP is a limiting factor to your video quality.) Setting the GOP too small can lead to blurry video because if the encoder is in a crunch, it will degrade QP. | Most encoders use a GOP length of 1-2 seconds, aka 30-60 frames @ 30fps, or 60-120 fps @60fps. [Default settings may differ in H264 & HEVC](https://openradar.appspot.com/FB7528508). Documentation falsely states that this property only applies to H264. |

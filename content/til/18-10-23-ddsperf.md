---
title           : "Cyclone's ddperf"
description     : "Tool for Cyclone DSS performane testing"
date            : 2023-10-18
katex           : false
draft           : false
---

`ddsperf` is a tool for benchmarking Cyclone DDS communication. Its functionality is pretty narrow yet perfectly fits the tool's purpose: publish and subscribe to messages sent within Cyclone + give statistics on that.

My experience with that tool was pretty short and was mostly about [that](https://github.com/ros2/rmw_cyclonedds/issues/461) issue.

I see myself ~~never debugging DDS problems ever again~~ using `ddsperf` for:

1. debugging ROS2 communication. 
Luckily it is not often the case in ROS2 when you need to dig deeper in the DDS level, but sometimes it is the case: you do not receive messages/service calls you expect or you have a non-standard hardware configuration something doesn’t work. It may be a good option to reproduce a problem with ddsperf only if possible to narrow down the root cause.
2. Curiosity.
It is always fun to check what are the theoretical limits of your system from a networking perspective (what happens if you send a 100MB/1Gb message? or 1000 messages per second?). If it is not fun, than I do not know what is!
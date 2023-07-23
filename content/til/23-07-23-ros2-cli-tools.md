---
title           : "Exploring ROS2 CLI: ros2 topic"
description     : "Stuff we do not often use from ros2 CLI"
date            : 2023-07-23
katex           : false
draft           : false
---

Sometimes we do not event realize how many useful tools are already available in ROS2. Today I learned about `ros2 topic` utils: `bw` and `delay`.

## ros2 topic bw

`ros2 topic bw` is a tool to measure bandwidth usage of a topic. Here is the how the otput looks like:

```bash
ros@dmitry:~$ ros2 topic bw /scan
Subscribed to [/scan]
202.10 KB/s from 34 messages
	Message size mean: 5.82 KB min: 5.82 KB max: 5.82 KB
199.97 KB/s from 68 messages
	Message size mean: 5.82 KB min: 5.82 KB max: 5.82 KB
199.13 KB/s from 100 messages
	Message size mean: 5.82 KB min: 5.82 KB max: 5.82 KB
199.30 KB/s from 100 messages
	Message size mean: 5.82 KB min: 5.82 KB max: 5.82 KB
199.61 KB/s from 100 messages
	Message size mean: 5.82 KB min: 5.82 KB max: 5.82 KB
```

That is a very usefull tool to build a better intuition about your robotics system. Yeah, we get used that poinclouds and images are usually the heaviest topic. But sometimes is not true: I worked on system where the heaviest topic was an `OccupancyGrid` representation of the map because the map of the environment was very large.

## ros2 topic delay

And one more tool for better undestanding of your robotics system: `ros2 topic delay`. Here is how the output looks like:

```bash
ros@dmitry:~$ ros2 topic delay /scan
average delay: 1690125329.740
	min: 1690125329.736s max: 1690125329.746s std dev: 0.00340s window: 33
average delay: 1690125329.746
	min: 1690125329.736s max: 1690125329.758s std dev: 0.00696s window: 67
average delay: 1690125329.751
	min: 1690125329.736s max: 1690125329.764s std dev: 0.00902s window: 102
average delay: 1690125329.756
	min: 1690125329.736s max: 1690125329.775s std dev: 0.01150s window: 136
```

_(The delay is so huge here because I do not how to enable simulated time for that tool ¯\_(ツ)_/¯)_

The way it works is very simple: it just compares the timestamp of the message with the current time. Basically what we get is the time difference between the moment when the message header timestamp was created and the moment when the message was received. So you need to know the code of publisher to be able to understand what is going on. But it is still a very useful tool to get a better understanding of your system.


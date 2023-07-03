---
title           : "Ring Buffer in Python and Robotics"
description     : "Shut up and use ring buffers"
date            : 2023-07-03
katex           : false
draft           : false
---

Today I Learned about a very simple way to get [ring buffer](https://www.wikiwand.com/en/Circular_buffer) data structure in Python: 

```python
from collections import deque

ring_buffer = deque(maxlen=5)
```

*Sometimes Python makes things boringly simple, isn’t it?*

I love `ring buffers`! They are the best choice (the only one?) as a buffer for streaming data and that is why they are frequent guests in certain types of robotics tasks. Let's consider a real example of data synchronization.

## Example

Let’s say you are programming a drone that does visual SLAM for localization. SLAM receives and processes 25 frames per second. SLAM also receives a GPS signal at 5Hz. So from time to time, you want to integrate GPS measurement (let’s call it GPS alignment) into SLAM to correct for drift if any exists.

So when you are ready to do GPS alignment you need to find the closest in time GPS measurement to the latest received image. To be able to do that you can keep a ring buffer with a certain maximum length. That will keep track of `N` latest GPS measurement. So when you need you just over that buffer and look for the closest measurement by comparing the time.
---
title           : "ROS2 Logging Levels"
description     : "Here is the firdt post"
date            : 2023-06-28
katex           : false
draft           : false
---

Today _(not today actually, but I want to write something, you know)_ I learned that setting ROS2 node logging level is not that obvious. Here is the story.

Imaging you have that annoying node that just doesn't want to work. 

So you decide to take the most unforgivable of all debugging methods: the `print`-based (or in ROS2 terms `RCLCPP_INFO`-based) debugging. And you want to do it right (ha-ha, naive boy, he thinks `print`-based one can be done right) and add more `debug`-level print statements (aka `RCLCPP_DEBUG`).

Now we need to run the node with the `debug` logging level.

_Quick_ glance at the [ROS 2 documentation](https://docs.ros.org/en/humble/Tutorials/Demos/Logging-and-logger-configuration.html#logger-level-configuration-command-line) and you have what you need (here is rviz2 run example):

```bash
ros2 run rviz2 rviz2 --ros-args --log-level debug 
```

Ok, ready to run, will make a tea whil.. OH MY GOD, WHAT IS GOING ON! WHY __EVERYHTING__ is in DEBUG NOW!?"


![hello](p3.jpg)

Here we come to the point : just passing `--log-level debug` 
> configures the default severity for any unset logger to the debug severity level. 
> You should see debug output from loggers from the node itself and from the ROS 2 core.

as they state in the doc. And that explains quite a lot.

But if you want to do it for a specific node, pass the node name to the `--log-level` argument:

```bash
ros2 run lzy_pkg lazy_node --ros-args --log-level lazy_node:=debug 
```

![hello](p2.jpg)

I didn't expect that behaviour.

I also didn't read the doc properly 😐

And that is what I learned today (not actually today, but I want to write something, you know).

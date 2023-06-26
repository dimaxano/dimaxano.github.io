---
title           : "ROS2 Logging Levels"
description     : "Here is the firdt post"
date            : 2023-06-27
katex           : false
draft           : true
---

Today _(not actually today, but I want to write something, you know)_ I learned that setting ROS2 node logging level is not that obvious.

Imaging you have that annoying node that just doesn't want to work. Let's call it a `lazy_node`:

```bash
ros2 run lzy_pkg lazy_node
```

So you decide to take the most unforgivable of all debugging methods: the `print`-based (or in ROS2 terms `RCLCPP_INFO`-based) debugging. And you want to do it right (ha-ha, naive boy, he thinks `print`-based one can be done right) and add more `debug`-level print statements (aka `RCLCPP_DEBUG`).

Okay, let's run that shit aaaand.. nothing new printed. 
Ah, I'm stupid, set the log level!

Quick glance at the ROS 2 documentation and you have what you need:

```bash
ros2 run lzy_pkg lazy_node --ros-args --log-level debug 
```

Ok, ready to run, will make a tea whil.. OH MY GOD, WHAT IS GOING ON! WHY __EVERYHTING__ is in DEBUG NOW!?"


For some reason to pass log-level to that specific node you need to specify that node name:

```bash
ros2 run lzy_pkg lazy_node --ros-args --log-level lazy_node:=debug 
```

I didn't expect that. And that is what I learned today (not actually today, but I want to write something, you know).

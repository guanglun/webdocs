---
title: i2c设备操作
date: 2021-06-24 22:56:35
categories: Linux
tags: 
    - Linux 
---

读取MPU6050 ID  
```
i2ctransfer -f -y 0 w1@0x68 0x75 r1
```
更多请看https://www.cnblogs.com/raina/p/12068485.html
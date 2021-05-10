---
title: autoconf.h自动包含问题
date: 2021-05-10 17:41:39
categories: Kernel
tags: 
    - Kernel
    - Linux 
---

[参考链接1](https://blog.csdn.net/qwaszx523/article/details/62234332)
[参考链接2](https://blog.csdn.net/zxl1217/article/details/3453196)

综合说一下，新版本的内核使用了自己的mkdep功能，用来自己预处理有关CONFIG_的宏定义，将之与在include/config下生成的空的头文件联系起来
  
理解如果有错，还望指出。
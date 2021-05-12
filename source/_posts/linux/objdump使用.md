---
title: objdump使用
date: 2021-05-10 19:36:18
categories: Linux
tags: 
    - Linux 
---

```
arm-linux-gnueabihf-objdump -s -d arch/arm/kernel/head.o > arch/arm/kernel/head.o.txt
```

对vmlinux反汇编的命令为：arm-linux-gnueabihf-objdump -dxh vmlinux > vmlinux.s

---
title: cpu_init
date: 2021-05-07 15:38:28
categories: kernelGenerate
tags: 
    - Linux 
    - Kernel
    - CodeNotes
---

[Code](https://github.com/guanglun/LinuxSoEasy/blob/master/arch/arm/kernel/setup.c#L522)
```c
void notrace cpu_init(void)
```
cpu_init

```c
unsigned int cpu = smp_processor_id();
```
smp_processor_id
---
title: start_kernel
date: 2021-05-07 15:38:28
categories: kernelGenerate
tags: 
    - Linux 
    - Kernel
    - CodeNotes
---

[Code](https://github.com/guanglun/LinuxSoEasy/blob/master/init/main.c#L848)
```c
asmlinkage __visible void __init __no_sanitize_address start_kernel(void)
```
start_kernelfcsad

```c
	char *command_line;
	char *after_dashes;
```
asdasdasdasdasdsadasd
```c
set_task_stack_end_magic(&init_task);
```

```c
debug_objects_early_init();
```

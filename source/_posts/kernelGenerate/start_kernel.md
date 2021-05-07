---
title: start_kernel
date: 2021-05-07 11:27:30
categories: kernelGenerate
tags: 
    - Linux 
    - Kernel
    - CodeNotes
---

```c
asmlinkage __visible void __init start_kernel(void)
```

```
* 顾名思义，内核启动函数

```c

```c

```
	char *command_line;
	char *after_dashes;* command_line指针定义
* after_dashes指针定义lockdep_init();
```c
set_task_stack_end_magic(&init_task);
```

```c
smp_setup_processor_id();
```

```c
debug_objects_early_init();
```

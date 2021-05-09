---
title: start_kernel
date: 2021-05-09 05:09:57
categories: kernelGenerate
---

|查看函数源码  |路径  |
|---|---|
|[SourceCode](https://github.com/guanglun/LinuxSoEasy/blob/master/init/main.c#L848)| /init/main.c |  
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

设置set_task_stack_end_magic(&init_task);

  
```c
debug_objects_early_init();
```  




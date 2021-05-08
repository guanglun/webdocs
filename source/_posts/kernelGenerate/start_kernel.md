---
title: start_kernel
date: 2021-05-08 18:02:35
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

* [查看set_task_stack_end_magic函数](http://www.guanglundz.com:8086/2021/05/08/kernelGenerate/set_task_stack_end_magic)  

设置set_task_stack_end_magic(&init_task);

  
```c
debug_objects_early_init();
```  




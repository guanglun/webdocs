---
title: set_task_stack_end_magic
date: 2021-05-09 05:09:57
categories: kernelGenerate
---

|查看函数源码  |路径  |
|---|---|
|[SourceCode](https://github.com/guanglun/LinuxSoEasy/blob/master/kernel/fork.c#L843)| /kernel/fork.c |  
```c
void set_task_stack_end_magic(struct task_struct *tsk)
```  

  

  
```c
stackend = end_of_stack(tsk);
```  

* [查看start_kernel函数](http://www.guanglundz.com:8086/2021/05/09/kernelGenerate/start_kernel)  

* [查看start_kernel函数](http://www.guanglundz.com:8086/2021/05/09/kernelGenerate/start_kernel)  




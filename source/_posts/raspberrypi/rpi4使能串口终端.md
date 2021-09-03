---
title: rpi4使能串口终端
date: 2021-06-04 12:27:17
categories: raspberrypi
tags: 
    - raspberrypi 
---

修改config.txt文件，再最后增加该行：
```
enable_uart=1
```

使用波特率115200  

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9zaHVtZWlwYWkubnhlei5jb20vd3AtY29udGVudC91cGxvYWRzLzIwMTUvMDMvcnBpLXBpbnMtNDAtMC5wbmc?x-oss-process=image/format,png)

![](https://img-blog.csdnimg.cn/20200530121909898.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3MjI0NTM0,size_16,color_FFFFFF,t_70)
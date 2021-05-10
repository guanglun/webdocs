---
title: autoconf.h自动包含问题
date: 2021-05-10 17:41:39
categories: Kernel
tags: 
    - Kernel
    - Linux 
---

[参考链接](https://blog.csdn.net/qwaszx523/article/details/62234332)


 执行make menuconfig后，编译系统会把所有的配置信息保存到源码顶层目录下的.config文件中，然后将.config中的内容转换为C语言能识别的宏定义更新到include/generated目录下的autoconf.h文件中。比如会将CONFIG_XXX =y的定义转换为#define CONFIG_XXX 1的模式写到autoconf.h文件当中。autoconf.h文件是被自动包含，不需要C代码文件中显式包含。在内核源码的根目录下的Makefile中实现了自动包含，顶层Makefile中相关的内容如下：

```
# Use LINUXINCLUDE when you must reference the include/ directory.
# Needed to be compatible with the O= option
LINUXINCLUDE    := -I$(srctree)/arch/$(hdr-arch)/include \
                   -Iarch/$(hdr-arch)/include/generated -Iinclude \
                   $(if $(KBUILD_SRC), -I$(srctree)/include) \
                   -include include/generated/autoconf.h 

............................

............................

............................

export KBUILD_CPPFLAGS NOSTDINC_FLAGS LINUXINCLUDE OBJCOPYFLAGS LDFLAGS
```
在LINUXINCLUDE赋值的最后一行包含了autoconf.h文件，然后通过export导出给其它的Makefile文件使用。
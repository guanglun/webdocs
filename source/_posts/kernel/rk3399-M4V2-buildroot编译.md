---
title: rk3399-M4V2-buildroot编译
date: 2021-05-18 22:01:38
categories: Kernel
tags: 
    - Kernel
    - Linux 
---
# buildroot编译生成镜像无法使用问题解决

* 将repo最顶层目录的build.sh脚本文件的  

```
flash=mmc,1:rootfs:ext4:0x6000000,${ROOTFS_PARTITION_SIZE}:rootfs.img; 
flash=mmc,1:userdata:ext4:${USERDATA_PARTITION_ADDR},0x0:userdata.img; 
```
两行修改成如下两行  
```
flash=mmc,1:rootfs:ext4:0x6000000,0x80000000:rootfs.img;  
flash=mmc,1:userdata:ext4:0x86000000,0x0:userdata.img;  
```

# 内核烧写使用dd指令(Kernel目录下操作)
```
sudo dd if=kernel.img of=/dev/sdb bs=1k seek=32768
```
# 烧写设备树等文件命令(Kernel目录下操作)
```
sudo dd if=resource.img of=/dev/sdb bs=1k seek=20480
```
# 编译Linux内核(Kernel目录下操作)
```
TOOLCHAIN_GCC=/home/guanglun/workspace/rk3399/linuxsdk-friendlyelec/prebuilts/gcc/linux-x86/aarch64/gcc-linaro-6.3.1-2017.05-x86_64_aarch64-linux-gnu/bin/aarch64-linux-gnu-
make ARCH=arm64 CROSS_COMPILE=${TOOLCHAIN_GCC} nanopi4-bootimg -j12
```  

# 编译报错处理
## debug_print ("SERVER: WaitingForBegin, read '%s'", line);报错
## debug_print ("SERVER: WaitingForBegin, read '%s'", line);报错
[http://www.cxyzjd.com/article/weixin_39697565/115109821](http://www.cxyzjd.com/article/weixin_39697565/115109821)
## _syscall0(int, gettid)报错
[https://patchew.org/QEMU/20190320122555.8025-1-berrange@redhat.com/](https://patchew.org/QEMU/20190320122555.8025-1-berrange@redhat.com/)

## SIOCGSTAMP报错
[https://patchwork.kernel.org/project/qemu-devel/patch/20190617114005.24603-1-berrange@redhat.com/](https://patchwork.kernel.org/project/qemu-devel/patch/20190617114005.24603-1-berrange@redhat.com/)


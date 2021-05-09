---
title: imx6ull-linux-kernel
date: 2021-05-09 14:13:03
categories: Kernel
tags: 
    - Kernel
    - Linux 
---

### 安装必要库
```
sudo apt-get install lzop libncurses5-dev
```
### 安装独立编译工具链
```
cd /opt
git clone https://github.com/guanglun/arm-gcc
vim ~/.bashrc
export PATH=$PATH:/opt/arm-gcc/bin/
source ~/.bashrc
```

### 编译

* 生成配置
```
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- imx_xly_defconfig
```

* 开始编译
```
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage -j12
```
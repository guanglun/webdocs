---
title: zynq笔记
date: 2021-06-16 15:44:56
categories: zynq
tags: 
    - zynq
---

# 使用echo_test
源于https://www.xilinx.com/support/documentation/sw_manuals/xilinx2017_1/ug1186-zynq-openamp-gsg.pdf page9  
```
echo image_echo_test > /sys/class/remoteproc/remoteproc0/firmware
echo start > /sys/class/remoteproc/remoteproc0/state
modprobe rpmsg_user_dev_driver
echo_test
```

# petalinux命令

```
source /opt/pkg/petalinux/settings.sh
petalinux-create --type project --template zynq --name amp
petalinux-config --get-hw-description ../linux_base.sdk
petalinux-config
petalinux-config -c kernel
petalinux-config -c rootfs
petalinux-build
petalinux-package --boot --fsbl ./images/linux/zynq_fsbl.elf --fpga --u-boot --force
cp images/linux/image.ub /mnt/hgfs/share/
cp images/linux/BOOT.BIN /mnt/hgfs/share/
```
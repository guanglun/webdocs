---
title: 在局域网建立.local域名
date: 2021-04-30 18:17:14
categories: Linux
tags: 
    - Linux 
    - ubuntu
---
* 安装
```
sudo apt-get install avahi-daemon
```
* 修改/etc/hosname
* 增加/etc/hosts
```
127.0.0.1       localhost
127.0.0.1       guanglun-tool
# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```


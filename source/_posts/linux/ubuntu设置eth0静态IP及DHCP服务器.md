---
title: ubuntu设置eth0静态IP及DHCP服务器
date: 2021-05-07 15:18:12
categories: Linux
tags: 
    - Linux 
    - Ubuntu
---


* 设置eth0静态IP
sudo vim /etc/network/interfaces
```
auto eth0
iface eth0 inet static
address 10.0.0.1
netmask 255.255.255.0
gateway 10.0.0.1
dns-nameservers 8.8.8.8
```

* 安装DHCP服务
```
sudo apt install isc-dhcp-server 
```

* 编辑/etc/default/isc-dhcp-server,设置监听对象
sudo vim /etc/default/isc-dhcp-server
```
INTERFACES="eth0" 
```

* 编辑DHCP服务器选项
sudo vim /etc/dhcp/dhcpd.conf 
```

option domain-name "mylab.com";
option domain-name-servers 10.0.0.1;

default-lease-time 3600;
max-lease-time 7200;



subnet 10.0.0.0 netmask 255.255.255.0 {
range 10.0.0.10 10.0.0.100;
option domain-name-servers 10.0.0.1;
option domain-name "mylab.com";
option subnet-mask 255.255.255.0;
option routers 10.0.0.1;
option broadcast-address 10.0.0.255;
default-lease-time 3600;
max-lease-time 7200;
}

```
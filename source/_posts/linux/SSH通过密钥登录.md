---
title: SSH通过密钥登录
date: 2021-05-06 09:54:50
categories: Linux
tags: 
    - Linux 
    - ssh
---
* 制作密钥对
首先在服务器上制作密钥对。首先用密码登录到你打算使用密钥登录的账户，然后执行以下命令：
```
ssh-keygen
```
接下来一直回车即可

* 在服务器上安装公钥
将.pub公钥‘注册’至服务器的公钥列表中
```
cat id_rsa.pub >> authorized_keys
```
* 设置SHH打开密钥登录功能
编辑 /etc/ssh/sshd_config 文件，进行如下设置
```
RSAAuthentication yes
PubkeyAuthentication yes
```
* 请留意 root 用户能否通过 SSH 登录
```
PermitRootLogin yes
```
* 密码登录开关
```
PasswordAuthentication no
```
* SSH服务重启
```
service sshd restart
```

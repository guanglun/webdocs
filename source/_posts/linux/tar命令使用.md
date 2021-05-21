---
title: tar命令使用
date: 2021-04-22 10:27:03
categories: Linux
tags: 
    - Linux 
    - 命令
---
## 常用tar命令查询
### 解压
```
tar -xzvf /tmp/etc.tar.gz <==解压到当前目录
tar -xzvf /tmp/etc.tar.gz -C /tmp <==解压到指定目录

tar.gz ： -xzvf
tar.bz2 ：-xjvf
```
### 打包压缩
```
tar -cvf /tmp/etc.tar /etc  <==仅打包，不压缩！
tar -czvf /tmp/etc.tar.gz /etc  <==打包后，以 gzip 压缩
tar -cjvf /tmp/etc.tar.bz2 /etc  <==打包后，以 bzip2 压缩
```   
## tar命令详解    
|||
|-|-|
|-c|压缩|
|-x|解压|
|-t|查看内容|

<br>  

|||
|-|-|
|v | 输出详情 |
|f | -f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名 |

<br>  

|||
|-|-|
|*.tar.xz | –xvf |
|*.tar.gz|–xzf|
|*.tar.bz2|–xjf|
|*.tar.Z|–xZf |


  

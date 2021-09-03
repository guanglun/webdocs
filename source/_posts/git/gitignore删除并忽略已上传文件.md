---
title: gitignore删除并忽略已上传文件
date: 2021-09-03 18:17:12
categories: Git
tags: 
    - git 
---

[参考链接](https://blog.csdn.net/luhu124541/article/details/82048357)
```
#清除本地缓存(改变成未track状态)
#git rm -r --cached . 表示清除项目中所有文件的本地缓存
git rm -r --cached xxx    #xxx表示不想版本控制的文件，比如小编可以输入test.o
                        #.gitignore中的忽略规则应该与之相对应
git add .   #添加除了忽略文件外的所有文件
git commit -m "此处可以描述你提交的信息"
git push -f #强制推送
```
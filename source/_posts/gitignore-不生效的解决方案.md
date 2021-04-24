---
title: .gitignore 不生效的解决方案
date: 2021-04-24 11:27:09
categories: Git使用
tags: 
    - git 
---


* 当我们将 .gitignore 文件配置好后，却往往不能失效。这是因为 .gitignore 只能忽略那些没有被追踪(track)的文件，因为 git 存在本地缓存，如果文件已经纳入了版本管理，那么修改 .gitignore 是不能失效的。那么解决方案就是要将 git 的本地缓存删除，然后重新提交。

```
git rm -r --cached .
git add .
git commit -m "update .gitignore"
```  

[参考链接](https://blog.csdn.net/zwkkkk1/article/details/83550032)  
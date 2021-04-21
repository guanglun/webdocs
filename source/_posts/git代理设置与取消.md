---
title: git代理设置与取消
date: 2021-04-21 15:54:43
tags:
---
* git代理设置与取消
```python
git config --global https.proxy http://127.0.0.1:1080

git config --global https.proxy https://127.0.0.1:1080

git config --global --unset http.proxy

git config --global --unset https.proxy
```
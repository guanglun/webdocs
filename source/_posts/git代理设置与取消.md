---
title: git代理设置与取消
date: 2021-04-21 15:54:43
tags:
categories: Git使用
---
* git代理设置与取消
```python
git config --global http.proxy 'socks5://127.0.0.1:10808'

git config --global https.proxy 'socks5://127.0.0.1:10808'

git config --global --unset http.proxy

git config --global --unset https.proxy
```
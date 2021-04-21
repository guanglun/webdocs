---
title: ubuntu下python版本切换
date: 2021-04-21 13:52:17
tags:
---
* 查看在usr目录里安装了几种不同版本的Python
```
$ ls /usr/bin/python*
```

* 创建符号链接
```python
sudo update-alternatives  --install /usr/bin/python python /usr/bin/python2.7 1
sudo update-alternatives  --install /usr/bin/python python /usr/bin/python3.5 2
```

* 切换Python版本
```python
sudo update-alternatives --config python
```

* 列出Python版本
```python
sudo update-alternatives --list python
```

* 查看Python版本
```python
python --version
```
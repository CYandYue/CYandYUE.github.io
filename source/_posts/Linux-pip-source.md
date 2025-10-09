---
title: pip换源
author: CYandYUE
index_img: /index_img/26_pip_source.png
date: 2025-10-09 18:44:05
tags:
- Env
- Shell
categories:
- Env
- Shell
---

## 0. Motivation
有时候换了服务器，pip下载时发现速度很慢很慢

实际上是因为忘了换源了

临时可以这样解决：

```bash
pip install name -i https://pypi.tuna.tsinghua.edu.cn/simple
```

各种国内源如下：
- 清华源：https://pypi.tuna.tsinghua.edu.cn/simple
- 阿里源：https://mirrors.aliyun.com/pypi/simple
- 豆瓣源：https://pypi.doubanio.com/simple

## 1. change pip source permanently
首先创建pip配置文件
```bash
mkdir -p ~/.pip
vim ~/.pip/pip.conf
```

写入以下内容
```bash
# in pip.conf
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
timeout = 600
```
---
title: vscode服务器无法选择python环境
author: CYandYUE
index_img: /index_img/17_vscode_ssh.png
date: 2025-03-17 03:51:26
tags:
- DEBUG
categories:
- DEBUG
---

## 1. 问题描述
用vscode ssh-remote连接服务器

发现右下角选择python解释器（conda环境中的）的选项消失了

导致高亮和跳转失效，读写代码不方便

## 2. 解决方案
上网查了一会

发现是本机vscode的版本太低了

从而导致本机的python扩展版本太低，与服务器上的拓展版本不兼容了

更新本机的vscode即可

我本机系统是Manjaro，只需要：
```bash
# 用yay装
$ yay -Sy isual-studio-code-bin
# 或者用paru
$ paru -Sy visual-studio-code-bin
```

## 3. Reference
[CSDN](https://blog.csdn.net/2401_86880265/article/details/143204956)
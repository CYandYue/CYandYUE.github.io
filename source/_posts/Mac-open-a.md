---
title: Mac-open-a
author: CYandYUE
index_img: /index_img/23_open_a.png
date: 2025-09-05 22:25:28
tags:
- Mac
categories:
- Mac
---

## 0. Motivation
今天想要在Mac上实现之前Manjaro那种在终端里打开vscode的效果

实际上很简单

## 1. Command "open -a"
Mac的程序是以application的形式储存在/Applications文件夹里

可以用"open -a"命令来打开

参数-a的意思是application

```bash
$ open -a "Visual Studio Code"
```
所以我们可以在.zhsrc文件里加上这一句alias
```bash
$ cd
$ vim .zshrc
```

```bash
# in .zshrc
alias code='open -a "Visual Studio Code"'
```

同理其他application也可以仿照
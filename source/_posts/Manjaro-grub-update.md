---
title: Arch Linux上更新grub
author: CYandYUE
index_img: /index_img/13_grub.png
date: 2025-03-02 00:28:22
tags:
- Linux
- Shell
categories:
- Linux
- Shell
---

## 1. Grub update in Arch Linux
在Ubuntu上更新grub的命令是：
```bash
$ sudo update-grub
```
实际上，update-grub 就是一个脚本，运行了 grub-mkconfig 包，生成了 grub.cfg

所以在ArchLinux上，当没有update-grub命令时，可以使用
```bash
$ grub-mkconfig -o /boot/grub/grub.cfg
```

## 2. Tips
我准备给这篇博客找个封面图

一搜grub，我才发现原来grub的意思是幼虫啊，挺贴切的

恐虫人士被吓晕了（悲

## 3. Reference
Stack overflow: https://unix.stackexchange.com/questions/111889/how-do-i-update-grub-in-arch-linux
Arch Document: https://wiki.archlinux.org/title/GRUB#Generate_the_main_configuration_file
---
title: "error: failed retrieving file 'community.db' from mirrors.xxx : The requested URL returned error: 404"
author: CYandYUE
index_img:
date: 2025-03-04 23:29:32
tags:
- Linux
- DEBUG
categories:
- Linux
- DEBUG
---

## 1. 问题描述
近日，在Manjaro上尝试更新：
```bash
$ sudo pacman -Syu
output:
:: Synchronizing package databases...
 core is up to date
 extra is up to date
 community.db failed to download
 multilib is up to date
 archlinuxcn is up to date
error: failed retrieving file 'community.db' from mirrors.tuna.tsinghua.edu.cn : The requested URL returned error: 404
error: failed to synchronize all databases (unexpected error)
```
可以看到，没办法从清华源拉取 community.db

我以为是源的问题，发现换源之后还是没法拉取，遂翻看论坛寻找解决方法

## 2. 解决方法
参考[Archlinux.org](https://archlinux.org/news/cleaning-up-old-repositories/)

可以发现其实两年前，[community]仓库已经被合并到[extra]了

为了保持更新不出错，[community]会维持空仓库的状态直到 2025-03-01

所以最近更新的时候会报这个错

解决办法就是在 /etc/pacman.conf 中将 [community] 部分注释掉
```bash
sudo vim /etc/pacman.conf

# in /etc/pacman.conf,comment out following lines:

# [community]
# SigLevel = PackageRequired
# Include = /etc/pacman.d/mirrolist
```

## 3. Reference
[Archlinux.topic](https://bbs.archlinux.org/viewtopic.php?id=303841)
[Archlinux.org](https://archlinux.org/news/cleaning-up-old-repositories/)

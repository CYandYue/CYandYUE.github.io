---
title: Zip聚合 分卷过的压缩文件
author: CYandYUE
date: 2025-03-01 22:46:17
index_img: /index_img/12_zip.png
tags:
- Linux
- Shell
categories:
- Linux
- Shell
---

## 1. 问题描述
最近跑项目下载一个数据集，因为数据集太大，作者将其分卷压缩了

我分别下载之后，突然意识到在linux上我不会用zip解压分卷的压缩文件

于是查阅资料，并写个博客记录一下

## 2. Zip
### 2.1 zip 解压缩 分卷文件
首先进行合并
```bash
$ zip -s 0 head.zip --out complete.zip
```
其中 -s 0 是合并分卷，head.zip是压缩文件的分卷头，complete.zip是合并的完整压缩文件

然后再解压即可
```bash
unzip complete.zip
```

### 2.2 zip 进行压缩文件分卷
2.1的逆过程
```bash
zip -r -s datasize name.zip folder/
```
其中datasize是分卷大小，例如 1m

## 3. Reference
https://blog.csdn.net/qq_19320227/article/details/127967543

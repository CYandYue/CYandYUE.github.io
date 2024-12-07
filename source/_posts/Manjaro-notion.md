---
title: Manjaro上使用Notion笔记
author: CYandYUE
date: 2024-12-08 07:13:42
index_img: /index_img/3_notion.png
tags:
- Manjaro
- 脚本

categories:
- 脚本
---

Notion是挺好用的笔记软件，但是其不支持 Manjaro

解决办法是写个脚本调用Notion的网页版，来实现在Manjaro上使用Notion

## 前置： 安装google chrome
```bash
yay -Sy google-chrome
```

## 调用Notion
首先创建一个脚本
```bash
touch notion.sh
```
编辑一下
```bash
vim notion.sh
```
写入以下内容
```bash
#!/bin/sh
cd /usr/bin
./google-chrome-stable --app=https://www.notion.so/login
```
以后直接跑脚本就行
```bash
sh notion.sh
```
也可以根据需求写进开机自启等
---
title: Ubuntu上安装Notion与Zotero
author: CYandYUE
index_img: /index_img/16_ubuntu_zotero_notion.png
date: 2025-03-05 22:39:52
tags:
- Env
- Ubuntu
categories:
- Env
- Ubuntu
---

## 1. 问题描述
最近本机装了个Ubuntu用来跑临时项目

打算装一下notion和zotero方便办公

写篇博客记录一下

## 2. Notion and Zotero
### 2.1 Notion
首先彻底清除本机上的notion残留
```bash
$ sudo apt purge notion*
```
然后就可以安装了
```bash
$ sudo snap install notion-snap-reborn
```

PS: 这里还提供第二种方法，但我尝试未成功（安装后打开一直白屏）
```bash
$ echo "deb [trusted=yes] https://apt.fury.io/notion-repackaged/ /" | sudo tee /etc/apt/sources.list.d/notion-repackaged.list
$ sudo apt update
$ sudo apt install notion-app-enhanced
$ sudo apt install notion-app
```

### 2.2 Zotero
ubuntu上的zotero一直由社区维护，详情可见[Zotero各平台安装文档](https://www.zotero.org/support/installation)

仓库地址为 https://github.com/retorquere/zotero-deb

安装步骤如下：
```bash
$ wget -qO- https://raw.githubusercontent.com/retorquere/zotero-deb/master/install.sh | sudo bash
$ sudo apt update
$ sudo apt install zotero
```

## 3. Reference
1. [Dev ahout notion](https://dev.to/gabrieladnz/install-notion-on-ubuntu-1nj5)

2. [Zotero各平台安装文档](https://www.zotero.org/support/installation)
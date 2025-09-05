---
title: Zotero+Onedrive云盘储存避免付费，插件zotMoov优化文件结构
author: CYandYUE
index_img: /index_img/22_zotero_onedrive_zotmoov.png
date: 2025-09-05 14:22:04
tags:
- Env
- Zotero
categories:
- Env
- Zotero
---

## 0. Motivation
昨天我在Mac上下载Zotero并进行同步时

发现Zotero的网盘上只有300M达到了上限

而超出的论文无法同步下来

所以我想将Zotero储存论文用的网盘迁移到Onedrive上

并利用Zotero插件zotMoov进行文件结构的优化，方便管理

## 1. Why zotMoov
首先我们要了解一下Zotero储存文件的结构

Zotero将一篇论文的本体（PDF等）与附件（笔记等）作为一个最小单元

并分配一个随机编码作为这个最小单元的文件夹名称

所以看起来会非常反人类，如下（想根据名字找论文管理非常麻烦）：
![Zotero file structure](Zotero_file.png)

插件zotMoov可以将论文的本体与附件差分出来管理，并用link建立连接

zotMoov管理的文件结构如下：
![zotMoov file structure](zotMoov_file.png)

## 2. Install zotMoov
在这里下载.xpi文件：[zotMoov github](https://github.com/wileyyugioh/zotmoov/blob/master/README.md)

然后打开Zotero，找到Tools-->Plugins-->齿轮图标，选择install plugins from files
![install plugins](install_from_files.png) 

找到刚刚下载的.xpi文件并安装即可

## 3. Onedrive
首先在电脑上安装Onedrive，Mac用户可以直接在应用超市里搜索安装

登陆你的用户，并选择一个文件夹当作Onedrive的同步文件夹

在该文件夹里创建一个用来放置Zotero文件的文件夹，名字可以叫做Zotero

## 4. Zotero Config
找到Zotero的settings（Mac为Preferences）

这里所有需要配置directories的都设置成Onedrive同步文件夹中我们刚创建的Zotero就行

先设置zotMoov的配置中的directories和settings
![zotMoov conifg](zotMoov_config.png) 

然后是sync的配置中，取消掉这两个settings
![sync conifg](sync_config.png) 

最后修改advanced配置中的Base directories
![advanced conifg](advanced_config.png) 

## 5. Move existing files
接下来我们要选中Zotero里所有的论文将其移动到Onedrive中

zotMoov做了很方便的适配

在Zotero中全选后点击右键，找到，如下：
![move files](move_files.png) 

## 6. Some errors
这时候你可能会发现还是有一些论文没有同步

这是因为你的另外的系统没有把文件传到Onedrive磁盘上

需要所有系统都按照1-5的流程配置一遍

## 7. Reference
[csdn blog](https://blog.csdn.net/weixin_50925658/article/details/146215901)
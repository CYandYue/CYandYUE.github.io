---
title: Blog迁移
author: CYandYUE
index_img: /index_img/21_hexo_migration.png
date: 2025-09-04 14:24:06
tags:
- Blog
categories:
- Blog
---

## 0. Background
今天打算将Manjaro上的Hexo博客仓库迁移到Mac来

记录一下遇到的问题

## 1. Install Hexo in Mac
首先要在Mac上安装[Hexo](https://github.com/hexojs/hexo)

Mac安装Hexo比linux简单一些，直接用brew安装即可

首先是安装brew包管理器
```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
# notice that you need to add sth in .zprofile following above command output
```

然后直接用brew安装
```bash
$ brew install hexo
```

## 2. Install Theme
如果原来的remote repo已经有主题的配置文件了，可以直接拉repo而不用安装主题

## 3. git clone remote repo
```bash
$ git clone xxxxxx
```

## 4. Some Errors
这时我们可能会发现使用如下Hexo命令时会出现报错
```bash
$ hexo new post xxx
$ hexo g
$ hexo s
```
```bash
output:
ERROR Cannot find module 'hexo' from '/Users/xx/my_blog' 
ERROR Local hexo loading failed in ~/my_blog 
ERROR Try running: 'rm -rf node_modules && npm install --force'
```
遇到上述报错直接按照提示的命令就可以解决问题
```bash
$ rm -rf node_modules
$ npm install --force
```
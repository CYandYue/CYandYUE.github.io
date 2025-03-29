---
title: 创建多个Github pages
author: CYandYUE
index_img: /index_img/18_github_pages.png
date: 2025-03-29 22:01:39
tags:
- Web
categories:
- Web 
---
## 1. 问题描述
前段时间用github pages做了一个个人博客

详情可见 [这篇](https://cy.terase.cn/2024/11/15/Manjaro%E9%83%A8%E7%BD%B2Hexo-Fluid/)

因为用的仓库是和git用户名重名的，当时以为github pages只能有一个

最近发现其实github pages能有多个，具体的配置过程如下

## 2. Github pages
###  2.1 创建仓库
首先创建一个仓库，名字自取

因为我这里是用来做个人主页，遂取名HomePage

在本地仓库关联远程一下

```bash
$ git remote add origin https://github.com/xxxxxx/HomePage.git
```

###  2.2 开启Github pages
接着在网页端的仓库页面找到：

settings -> Pages -> Build and deployment -> source这个选项

选择Github actions

### 2.3 配置actions configure
还是在仓库页面找到：

Actions

点进去之后git会根据你的仓库代码推荐最合适的配置

像我这里的html做静态网页，所以选择的是Static HTML

如果没有特殊需求，就用默认配置即可（配置的是服务器的设置）

点击configure之后，git会在你的仓库里生成一个隐藏文件夹 .github/workflows

里面存放Actions的yml配置文件

### 2.4 部署
还是在仓库页面找到：

Actions

左边能看到现在的workflow，点击进去

再点击Run workdlow

就可以看到git正在编译部署你的仓库，比如我这里就是在编译我的静态页面

完成后会给出一个网址，点进去就可以看到页面了（关于这个详见2.5）

### 2.5 Custom domain
在网页端的仓库页面找到：

settings -> Pages -> Custom domain

这里可以配置pages的网址

但是我之前CYandYue/CYandYue仓库的github pages配置过了域名cy.terase.cn

这次CYandYue/HomePage仓库就不用再配置了

git会直接用路径形式将page挂在cy.terase.cn/HomePage上

## 3. Reference
效果可以参见我的[个人页面](https://cy.terase.cn/HomePage)及其[仓库](https://github.com/CYandYue/HomePage)
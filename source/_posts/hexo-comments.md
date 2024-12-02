---
title: Hexo评论功能插件Valine
author: CYandYUE
date: 2024-12-02 23:17:51
tags:
- 环境配置
- 博客

index_img: /index_img/2_valine.png

categories:
- 环境配置
- 博客
---

今天决定给自己的博客弄个评论功能，浏览了一下Hexo Fluid支持的评论插件，感觉Valine是比较好的选择

Valine的优点有：
- 快速高校，风格简约
- 无后端（轻量方便，核心原因）

下面是踩坑过程

## 1. 前置：LeanCloud数据库
valine要用到LeanCloud数据库储存评论数据，先开一个LeanCloud仓库

### LeanCloud注册
首先在LeanCloud[注册](https://console.leancloud.cn/register)或[登录](https://console.leancloud.cn/login)

注册要实名认证，还要支付宝扫码认证，和诈骗有点像(bushi)，能不能换种方式hhh

### LeanCloud仓库
进入[控制台](https://console.leancloud.cn/apps)，点击左上角的create

![创建仓库](leancloud_1.jpg)

<p id="1"></p> 

应用创建好以后，进入刚刚创建的仓库，选择左边的设置>应用凭证，记录AppID和AppKey：


![创建仓库](leancloud_2.jpg)


### LeanCloud域名设置
在仓库的设置>安全中心>Web 安全域名中添加博客的域名

Valine有请求限制，非安全域名的请求其不会放行

但是只在localhost测试时可以不设置安全域名

## 2. 开放Valine评论系统
### Fuild主题开放评论功能
在Fuild主题配置文件_config.fluid.yml中找到comments一栏

将enable改成true，type选择valine

```yaml
  # 评论插件
  comments:
    enable: true
    # 指定的插件，需要同时设置对应插件的必要参数
    # Options: utterances | disqus | gitalk | valine | waline ......
    type: valine
```

### Valine配置
_config.fluid.yml中，找到valine的配置，将[此处](#1)记录的AppID和AppKey填进配置

```yaml
# Valine
# 基于 LeanCloud
# See: https://valine.js.org/
valine:
  appId: your leancloud id         # 必填
  appKey: your leancloud key       # 必填
  path: window.location.pathname
  placeholder:
  avatar: 'retro'
  meta: ['nick', 'mail', 'link']
  requiredFields: []
  pageSize: 10                    # 一页的评论数
  lang: 'zh-CN'                   # 语言
  highlight: false
  recordIP: false
  serverURLs: ''
  emojiCDN:
  emojiMaps:
  enableQQ: false
  visitor: true                    # 统计阅读量功能，可以打开
```
别的配置可以参考Valine[官方文档](https://valine.js.org/configuration.html)


## 3. 评论管理
由于Valine是没有后端的server，所以其本身没有集成评论管理功能

但是我们可以直接在LeanCloud的数据库进行评论数据的管理操作

例如要删除评论的话，我们可以：

登录LeanCloud>选择你创建的仓库>数据存储>结构化数据>选择Class Comment>勾选删除

如果遇到下列类似的报错
```bash
Error: Forbidden writing by object‘s ACL.
```
可以在对应评论的“ACL”处将write权限开放，再进行操作

## 4. 链接
### 参考文档
- [Valine官方文档](https://valine.js.org/)
- [Csdn博客](https://blog.csdn.net/raspi_fans/article/details/134102368)
### 网址汇总
- [LeanCloud](https://console.leancloud.cn/apps)
---
title: 用ZeroOmega在多个proxy中自动切换
author: CYandYUE
index_img: /index_img/
date: 2026-01-04 18:18:33
tags:
- Web
categories:
- Web
---

## 0. Motivation
根据具体的网址来决定走不走代理，走什么代理，一直都是一个很实用的需求

浏览器上可以用Chrome的ZeroOmega插件来实现

## 1. Installtion
在Chrome插件商店里找到[ZeroOmega](https://chromewebstore.google.com/detail/proxy-switchyomega-3-zero/pfnededegaaopdmhkdmcofjmoldfiped?hl=en-US&utm_source=ext_sidebar)并安装

## 2. Config
找到插件的Options

![点击Options](options.jpg)

左侧点击proxy，填入你的代理的端口，通常可见代理软件设置

![配置Proxy](proxy.jpg)

然后点击左侧的auto switch

首先将default设置成走proxy代理，这会导致所有你没有特殊指定的网站走proxy代理

然后将特殊的需要直连的网址设置成走Direct（这里Host Wildcard是一直匹配策略）

![配置具体的switch策略](switch.jpg)

当然你也可以默认直连，特殊网址走代理，或者直接导入他人写好的switch策略，具体视需求而定

## 3. Use
现在在右上角使用auto-switch策略就可以生效了
![使用switch策略](use.jpg)
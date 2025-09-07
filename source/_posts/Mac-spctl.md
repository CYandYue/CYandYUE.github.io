---
title: Mac使用spctl取消对"allow applications from anywhere"的隐藏
author: CYandYUE
index_img: /index_img/24_spctl.png
date: 2025-09-07 23:30:56
tags:
- Mac
categories:
- Mac
---

## 0. Background
今天在安装一个插件的时候发现系统提醒：

无法打开“xxx”，因为无法验证开发者

本来可以直接在Mac的设置里允许信任任何来源的applications

但是从macOS Sierra (10.12)开始，Mac默认隐藏了"任何来源"选项

需要用spctl打开

## 1. Solution
打开终端输入
```bash
sudo spctl --master-disable
```
spctl是Security Assessment Policy Control的缩写，用来控制 Gatekeeper 安全功能

接着你会看到如下输出提示：
```txt
Output:
Globally disabling the assessment system needs to be confirmed in System Settings.Globally disabling the assessment system needs to be confirmed in System Settings
```
接着就可以在系统设置里找到选项了

找到 Apple —> System Settings —> Privacy&Security —> Allow applications from, 选择 “anywhere” 即可
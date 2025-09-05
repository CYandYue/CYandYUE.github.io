---
title: Mac使用applescript自定义Action与快捷键
author: CYandYUE
index_img: /index_img/20_applescript.jpg
date: 2025-09-04 13:05:57
tags:
- Mac
categories:
- Mac
---

## 0. Motivation
今天第一次用MacOS，发现command+space的Spotlight功能很好用

可以搜索文件/程序并打开

但是这样开终端还是太慢了

所以研究了一下如何把“开终端”设计成一个Action并绑定快捷键

## 1. Applescript Workflow
首先在launchpad里搜索到应用--Automator
![Automator Application](Automator.png)

打开Automator，点击Quick Action
![Quick Action](quick_action.png)

在左上角搜索run applescript，点击Run Applescript
![Run Applescript](Run_Applescript.png)

编写script，记得把右上角的input改成None
![write script](script.png)

按下command+s保存action，名字为Quick Open Terminal

找到系统设置System Settings
![setting](settings.png)

找到键盘设置，点击Keyboard Shortcuts
![keyboard](keyboard.png)

找到Services -->  General --> Quick Open Terminal，按下enter开始绑定快捷键即可
![shortcut](shortcut.png)

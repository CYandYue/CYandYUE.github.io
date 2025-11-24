---
title: Linux终端复用器Screen的主题配置.screenrc
author: CYandYUE
index_img: /index_img/29_screen_theme.jpg
date: 2025-11-21 23:34:39
tags:
- Linux
categories:
- Linux
---

## 0. Motivation
最近在服务器上用screen

发现如果采用默认的设置，ctrl+a+c创建窗口之后，没有窗口的标识

非常难分辨

所以打算抄一个好用的设置

## 1. Screen config
首先找到screen的配置文件 .screenrc

一般是 $HOME/.screenrc

如果没有的话，可以创建一个

首先进入$HOME
```bash
cd 
```

然后创建
```bash
touch .screenrc
```

然后打开
```bash
vim .screenrc
```

写入以下内容
```bash
# in .screenrc
# Set default encoding using utf8
defutf8 on


## 解决中文乱码,这个要按需配置
defencoding utf8
encoding utf8 utf8
 

#兼容shell 使得.bashrc .profile /etc/profile等里面的别名等设置生效
shell -$SHELL

#set the startup message
startup_message off
# term linux

## 解决无法滚动
termcapinfo xterm|xterms|xs ti@:te=\E[2J
 
# 屏幕缓冲区行数
defscrollback 10000
 
# 下标签设置
hardstatus on
caption always "%{= kw}%-w%{= kG}%{+b}[%n %t]%{-b}%{= kw}%+w %=%d %M %0c %{g}%H%{-}"
 
#关闭闪屏
vbell off
 
#Keboard binding
# bind Alt+z to move to previous window
bindkey ^[z prev
# bind Alt+x to move to next window
bindkey ^[x next

# bind Alt`~= to screen0~12
bindkey "^[`" select 0
bindkey "^[1" select 1
bindkey "^[2" select 2
bindkey "^[3" select 3
bindkey "^[4" select 4
bindkey "^[5" select 5
bindkey "^[6" select 6
bindkey "^[7" select 7
bindkey "^[8" select 8
bindkey "^[9" select 9
bindkey "^[0" select 10
bindkey "^[-" select 11
bindkey "^[=" select 12
# bind F5 to create a new screen
bindkey -k k5 screen
# bind F6 to detach screen session (to background)
bindkey -k k6 detach
# bind F7 to kill current screen window
bindkey -k k7 kill
# bind F8 to rename current screen window
bindkey -k k8 title
```
最后创建一个新的后台就可以看到效果了
---
title: Manjaro上使用xrandr外接显示器
author: CYandYUE
index_img: /index_img/19_xrandr.jpeg
date: 2025-07-15 19:27:17
tags:
- Manjaro
- Shell
categories:
- Manjaro
- Shell
---
最近提前进组开始博士生涯了

学校硬件设备很好，图书馆能白嫖显示器

突然想着写一下关于xrandr配置外接显示器的博客

也给自己做笔记了

## 1. xrandr检测设备
直接xrandr就可以看到各种设备的分辨率和刷新频率等信息
```bash
$ xrandr
output:
Screen 0: minimum 320 x 200, current 2560 x 1600, maximum 16384 x 16384
eDP-1 connected primary 2560x1600+0+0 (normal left inverted right x axis y axis) 345mm x 215mm
   2560x1600    240.00*+  60.00 +  59.99    59.97
   2560x1440     59.99    59.99    59.96    59.95
   2048x1536     85.00    75.00    60.00
   1920x1440     85.00    75.00    60.00
   ......
DP-1-0 disconnected (normal left inverted right x axis y axis)
DP-1-1 disconnected (normal left inverted right x axis y axis)
HDMI-1-0 connected (normal left inverted right x axis y axis)
   1920x1080     60.00 + 100.00    74.97    59.94    50.00
   1680x1050     59.95
   1600x900      60.00
   ......
DP-1-2 disconnected (normal left inverted right x axis y axis)
  1680x1050 (0x65) 146.250MHz -HSync +VSync
        h: width  1680 start 1784 end 1960 total 2240 skew    0 clock  65.29KHz
        v: height 1050 start 1053 end 1059 total 1089           clock  59.95Hz
  1280x1024 (0x6e) 135.000MHz +HSync +VSync
        h: width  1280 start 1296 end 1440 total 1688 skew    0 clock  79.98KHz
        v: height 1024 start 1025 end 1028 total 1066           clock  75.02Hz
  ......
```
可以看出主显示器是 eDP-1，外接显示器是 HDMI-1-0

## 2. 输出并指定显示器布局
可以使用下列命令将 HDMI-1-0 设置在 eDP-1 上方
```bash
xrandr --output HDMI-1-0 --auto --above eDP-1
# auto是自动配置分辨率
```
其他常见的布局有
```bash
--right-of eDP-1: 设置在右侧

--left-of eDP-1: 设置在左侧

--below eDP-1: 设置在下方

--same-as eDP-1: 镜像显示
```

## 3. 关闭到外接显示器的输出
使用--off参数即可
```bash
xrandr --output HDMI-1 --off
```
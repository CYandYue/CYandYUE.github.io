---
title: 'Manjaro蓝牙BUG：Bluetooth: hci0: Failed to load Intel firmware file intel/ibt-0040-1050.sfi (-2)'
author: CYandYUE
date: 2024-12-24 03:36:48
index_img:
tags:
- DEBUG
- Manjaro
categories:
- DEBUG
---

## 1. 问题描述
昨天用Manjaro的时候突然发现Bluetooth manager寄了，图形化界面直接没了

尝试用命令行的方式连接，发现bluetoothctl也找不到controller
![蓝牙失效了](bluetooth_bug_1.png)

## 2. 排查过程
### 2.1 查看bluetooth.service的状态
```bash
$ sudo systemctl status bluetooth
# output: 
bluetooth.service - Bluetooth service
Loaded: loaded (/usr/lib/systemd/system/bluetooth.service; enabled; preset: disabled)
Active: active (running)
```
发现是enable + activate，说明服务状态是正常的

若不正常，可使用
```bash
$ sudo systemctl start bluetooth  # 启动服务
$ sudo systemctl enable bluetooth # 设置为开机自启
```

### 2.2 查看无线设备状态
```bash
$ sudo rfkill list
# output:
0: hci0: Bluetooth
	Soft blocked: no
	Hard blocked: no
1: phy0: Wireless LAN
	Soft blocked: no
	Hard blocked: no
```
说明没有软禁用

如发现有 'Soft blocked: yes'，可以使用下列方式解锁软件禁用
```bash
sudo rfkill unblock bluetooth
```

### 2.3 使用sudo bluetoothctl
在网上看到有使用sudo bluetoothctl的说法，尝试后无果

### 2.4 dmesg查看内核缓冲区log
好友提醒我看看dmesg，终于找到了问题所在
```bash
sudo dmesg
```
![dmesg输出](bluetooth_bug_2.png)

log显示 : 'Bluetooth: hci0: Failed to load Intel firmware file intel/ibt-0040-1050.sfi (-2)'

## 3. 解决方案
在论坛上看到有人说是缺了firmware的固件，可以git拉去，或者直接下载放到对应的地方

![大神救我](bluetooth_bug_3.png)

于是我在[firmware下载地址](https://anduin.linuxfromscratch.org/sources/linux-firmware/intel/)下载了缺少的固件

并放到了 /lib/firmware/intel 中

终于解决了问题

![bluetoothctl输出正常](bluetooth_bug_4.png)

至于为什么缺少固件还没时间仔细研究

一直感觉 Manjaro 什么都好，但是蓝牙真的不太好用，流眼泪了


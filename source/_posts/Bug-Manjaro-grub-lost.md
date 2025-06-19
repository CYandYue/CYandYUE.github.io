---
title: Manjaro的grub引导掉了
author: CYandYUE
index_img:
date: 2025-06-19 15:11:27
tags:
- DEBUG
categories:
- DEBUG
---

## 1. 问题描述
最近使用windows时，若电脑自然掉电，就会导致我的manjaro grub直接消失，非常神秘

这里记录一下怎么依靠启动盘修复manjaro的grub

## 2. 解决方案
### 2.1 启动盘制作
首先要使用一个格式化的U盘制成启动盘

1. 下载镜像：由于我用的是Manjaro i3，在[Manjaro官网](https://manjaro.org/products/download/x86)的Community Images中，选择i3 Window Manager进行下载
2. 下载启动盘制作软件：我用的是Rufus，免费的启动盘制作软件，可以在[Rufus官网](https://rufus.ie/en/)进行下载
3. 制作启动盘：插入U盘，打开Rufus，导入镜像，开始制作，等待完成即可拔出

### 2.2 启动盘引导
需要用启动盘引导Manjaro启动
1. 将电脑关机
2. 开机时按F2或者F10进入BIOS界面
3. 将U盘引导调至最优先
4. 保存BIOS设置退出
5. 等待一段时间，这时Manjaro的引导界面应该已经出现了，选择start with open resources进入试用的Manjaro系统
   
### 2.3 chroot进行grub修复
system + ENTER 进入终端

使用chroot自动检测并挂载已安装的Linux系统
```shell
sudo manjaro-chroot -a 
# 此时应该已经切换到已经安装的Manjaro系统的根目录了
```
```markdown
chroot并非manjaro的独有命令

manjaro-chroot是manjaro提供的基于arch-chroot的一个脚本工具

-a 意思是auto，会扫描所有已挂载的分区，列出可用的系统，然后让你选择要 chroot 进入哪一个
```

接着可以进行grub的修复
```shell
# 首先更新grub
sudo pacman -Syu grub

# 将 GRUB 启动引导程序写入EFI分区中
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=manjaro --recheck

# 重新生成 grub.cfg 配置文件，告诉 GRUB 启动菜单怎么显示、要加载哪些系统
# 等效于自动脚本sudo update-grub
grub-mkconfig -o /boot/grub/grub.cfg
```
接着：
1. 关机，拔掉U盘
2. 开机的过程中按F2或者F10进入BIOS界面
3. 调整启动项，可以发现现在多了一个启动项叫manjaro了，将其调至最优先
4. 保存退出BIOS
5. 恢复正常

## 3. Reference
[1.个人博客](https://yangchnet.github.io/Dessert/posts/linux/manjaro%E6%81%A2%E5%A4%8Dgrub/)

## 4. 后记
关于为什么会出现“使用windows时，若电脑自然掉电，就会导致我的manjaro grub直接消失”这一现象

原因暂时不明，后续若排查出结果会更新博客
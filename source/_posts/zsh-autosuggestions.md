---
title: zsh-autosuggestions和syntax-highlighting
author: CYandYUE
date: 2024-12-27 05:29:32
index_img: /index_img/7_zsh.png
tags:
- 环境配置
- Shell
categories:
- 环境配置
- Shell
- Linux
---

本来大二的时候装完[oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh)，给自己的zsh美化了一下之后，想再装一个[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions?tab=readme-ov-file)自动补全

后来想想，感觉这东西和copilot是一个性质的，会让人产生依赖性

正巧当时还刚接触Linux，为了锻炼自己，最后是忍住了没装

今天觉得是时候了\(bushi

顺便再安装一个高亮[zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting?tab=readme-ov-file)

遂记录一下

## 0. oh-my-zsh
太久之前弄得了，哪天重新配的时候再记录吧，防止有错

## 1. zsh-autosuggestions
基于oh-my-zsh，首先找到oh-my-zsh插件路径
```bash
$ cd .oh-my-zsh/custom/plugins
```
拉取仓库
```bash
$ git clone https://github.com/zsh-users/zsh-autosuggestions
```
在 .zshrc 中加上插件配置(plugins那行)
```bash
# in .zshrc
plugins=(
        # ... other plugins ...
        zsh-autosuggestions
)
```
完成

## 2. zsh-syntax-highlighting
同理
```bash
$ cd .oh-my-zsh/custom/plugins
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
```
```bash
# in .zshrc
plugins=(
        # ... other plugins ...
        zsh-syntax-highlighting
)
```
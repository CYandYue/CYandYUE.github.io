---
title: 用GNU-stow集中管理dotfiles
author: CYandYUE
date: 2025-1-18 03:01:54
index_img: /index_img/10_dotfiles.png
tags:
- Shell
categories:
- Env
- Shell
---

最近经常自己搞搞配置，比如 .vimrc .tmux.conf .i3/config 之类的

想把这些 dotfiles 集中放在一个文件夹，用git管理，也方便之后换电脑快速配置

但是用 ln 一个一个手动把文件夹中的 dotfiles 链接回用户目录下明显是不现实的 

例如 oh-my-zsh 的配置可能是递归的多层文件夹，手动操作太麻烦了

这时候就需要像 gnu-stow 这样的工具

## 1. install stow
我是用的是 manjaro(Arch), 直接用pacman安装即可
```bash
$ sudo pacman -Sy stow
```
其他系统可自行查阅对应的安装方法

## 2. dotfiles management
### 2.1 new dir
为了集中管理 dotfiles, 首先可以在用户目录下新建一个文件夹用于存放所有 dotfiles
```bash
$ cd
$ mkdir .dotfiles # any name is ok
```

### 2.2 move dotfiles 
接下来将 dotfiles 转移到刚才新建的文件夹下

由于 stow 的管理单元是一个一个的 package

我们需要在 .dotfiles/ 下创建对应的文件夹当作 package

#### single file
像 .zshrc 这种单个配置文件，直接转移就好（注意提前做好备份）

```bash
# for backup
$ cd
$ cp .zshrc .zshrc_

# new stow package
$ cd .dotfiles
$ mkdir zsh

# mv 
$ mv ../.zshrc ./zsh
```
接着用stow创建软链接
```bash
$ stow zsh
```
我们可以回到用户目录下，看看是否成功
```bash
$ cd
$ ls -al | grep zshrc
output:
.zshrc -> .dotfilrs/zsh/.zshrc # the symlink is right here
```

#### recursive dotfiles
上述单个文件用stow管理，可能会觉得好像这没什么方便的啊

但是当遇到以下情景时，stow的优势就体现出来了
```bash
$ tree
output:
/home/username/.recursive_config
├── config_1
└── A
    ├── config_2
    │   ├── ...
    │   ├── ...
    │   └── ...
    │
    └── B
        ├── config_3
        │   └── ...
        │
        ├── config_4
        │   └──...
        │
        └── C
            └── config_5
```
这时候一个一个自己链接就太慢了
可以直接将整个文件夹转移到 stow 的 package 中，再用 stow 递归链接
```bash
$ cd
$ mkdir .dotfiles/A
$ mv .recursive_config .dotfiles/A
$ stow A
```

## 3. My dotfiles
我最近刚建了个仓库，但是里面配置文件还没仔细自己写，先放个[链接](https://github.com/CYandYue/dotfiles)在这，以后这个仓库会更新的
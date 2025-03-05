---
title: Vim的进阶配置和插件
author: CYandYUE
date: 2024-12-30 03:01:54
index_img: /index_img/9_vim.png
tags:
- Env
- Shell
categories:
- Env
- Shell
---

最近感觉自己vim用的还是太浅薄了，决定初步改一下配置并装一些好用的插件

平时使用vim的时候是否出现过以下问题：
- 想跳到某行，得先数现在光标到该行的距离 n，再使用 n j/k （count功能）
- 在vim里不方便切换文件，得退出vim切换文件再打开
- 单个windows的时候没有状态栏显示，忘记自己在哪个文件里

跟着本博客即可解决这些问题

## 1. Vim config: .vimrc
首先可以用默认配置文件开启一些隐藏的可选项，比如显示相对行距
在用户目录下新建隐藏文件 .vimrc
```bash
$ vim .vimrc
```

将下列配置写进 .vimrc
```.vimrc
" Comments in Vimscript start with a `"`.

" 关闭与vim的兼容模式，否则为了兼容会让很多强大的功能失效
set nocompatible

" 开启高亮
syntax on

" 禁用默认的 Vim 启动消息，简洁
set shortmess+=I

" 显示光标所在行
set number

" 显示相对行距，方便使用 count 功能
set relativenumber

" 即使只打开一个窗口，也始终在底部显示状态
set laststatus=2

" 默认情况下，不能在用“i”设置的插入点之前退格。此设置旨在解决这种问题
set backspace=indent,eol,start

" 允许在有未保存的情况下切换buffer，此时vim将负责直接保存
set hidden

" 搜索时忽略大小写
set ignorecase
set smartcase

" 进行搜索时，仍在打字阶段就开始搜索
set incsearch

" 取消无用的按键绑定
nmap Q <Nop> " 'Q' in normal mode enters Ex mode. You almost never want this.

" 禁用铃声
set noerrorbells visualbell t_vb=

" 开启鼠标模式，有时候会方便很多
set mouse+=a

" normal mode中，防止使用上下左右的方向键，养成好习惯
nnoremap <Left>  :echoe "Use h"<CR>
nnoremap <Right> :echoe "Use l"<CR>
nnoremap <Up>    :echoe "Use k"<CR>
nnoremap <Down>  :echoe "Use j"<CR>
" insert mode中也是如此
inoremap <Left>  <ESC>:echoe "Use h"<CR>
inoremap <Right> <ESC>:echoe "Use l"<CR>
inoremap <Up>    <ESC>:echoe "Use k"<CR>
inoremap <Down>  <ESC>:echoe "Use j"<CR>

```
此时新开一个终端，再使用vim打开 .vimrc，是不是发现了新天地

## 2. Vim plugins
可以安装一些好用的vim插件，这里我推荐一个：[CtrlP（模糊文件查找）](https://github.com/ctrlpvim/ctrlp.vim)
```bash
$ mkdir -p ~/.vim/pack/plugins/start
$ git clone --depth=1 https://github.com/ctrlpvim/ctrlp.vim.git ~/.vim/pack/plugins/start/ctrlp
```
此时用vim打开一个文件，使用command模式键入 :CtrlP，会发现已经可以使用文件搜索了，筛选完成后按Enter打开文件

为了更方便使用，可以在 .vimrc 中绑定快捷键
```.vimrc
" 插件 CtrlP 来实现vim内文件搜索和打开
let g:ctrlp_map = '<c-p>' " 快捷键 ctrl + p 打开插件
let g:ctrlp_cmd = 'CtrlP' " command模式, 键入 :CtrlP 
```
此时新开终端，使用快捷键 ctrl + p，就可以使用模糊文件查找了

## 3. 后记
随着我自己对vim的使用，我会更新自己的配置

同时介绍更多好用的插件给大家

后续有空了，还会出一篇长文介绍高效使用vim的技巧
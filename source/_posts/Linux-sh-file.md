---
title: Linux直接执行与调用解释器的权限区别
author: CYandYUE
date: 2024-12-23 00:24:32
index_img: /index_img/5_sh_file.png
tags:
- Linux
- Shell
categories:
- Linux
- Shell
---

今天做作业，发现了一个有趣的权限问题

## 1. 问题描述
```bash
$ ls -l
-rw-rw-r-- 1 cy cy 61 Dec 22 23:54 semester

$ cat semester
#!/bin/sh
curl --head --silent https://missing.csail.mit.edu
```
可以看到semester是一个获取http头部响应的程序，但是其没有execute权限

如果直接运行程序，自然是不行的，如下
```bash
$ ./semester
zsh: permission denied: ./semester
```
但是使用shell则可以，如下
```bash
$ sh semester
HTTP/2 200 
server: GitHub.com
content-type: text/html; charset=utf-8
last-modified: Sat, 21 Dec 2024 16:53:01 GMT
......
```
这是为什么呢

## 2. 直接执行 与 调用解释器
经过一番查阅发现，这是因为文件的执行权限（x）和解释器调用的方式不同
### 直接执行
- 权限要求: 需要执行权限（x）
- 行为： 直接尝试执行文件，系统检查权限并确认文件类型（如 ELF 二进制或脚本）。
  
### 调用解释器
- 权限要求：需要读取权限 (r)
- 行为：调用 sh 解释器，解释器读取文件内容并执行每一行的指令。

### 回到问题
所以上述情况能使用sh file的原因是：

使用 sh 时，不依赖文件的执行权限（x），而是依赖读取权限 (r)。

这是因为 sh 作为解释器，直接读取文件内容并按脚本语法逐行执行，而不是尝试将文件作为一个独立的可执行程序运行。
---
title: Git配置文件.gitconfig
author: CYandYUE
index_img: /index_img/15_gitconfig.png
date: 2025-03-04 23:54:38
tags:
categories:
---
## 1. 问题描述
最近项目中涉及很多比较大的仓库的拉取，同时我的网络又不够稳定

在 .gitconfig中修改配置，可以解决大部分问题

## 2. Git配置
### 2.1 .gitconfig
首先可以看看用户目录下有没有 .gitconfig 这个文件
```bash
$ cd ~
$ ls -a | grep gitconfig
```
没有的话自己创建一个也可以
```bash
$ cd ~
$ touch .gitconfig
```
### 2.2 问题1: early EOF fatal
有时候 git clone 会出现下列报错
```bash
$ git clone xxxxxxx
output:
Cloning into 'xxxxxx'...
remote: Counting objects: 4846, done.
remote: Compressing objects: 100% (3256/3256), done.
fatal: read error: Invalid argument, 255.05 MiB | 1.35 MiB/s
fatal: early EOF
fatal: index-pack failed
```
可以在 .gitconfig 中添加下面这段配置
```bash
$ vim .gitconfig

# in .gitconfig add the following lines:
[core] 
packedGitLimit = 512m 
packedGitWindowSize = 512m 
[pack] 
deltaCacheSize = 2047m 
packSizeLimit = 2047m 
windowMemory = 2047m
```

### 2.3 问题2: he remote end hung up unexpectedly
要是 git clone 时出现下列报错：
```bash
error: RPC failed; curl 56 GnuTLS recv error (-12): A TLS fatal alert has been received.
fatal: The remote end hung up unexpectedly
fatal: The remote end hung up unexpectedly
Everything up-to-date
```
有可能是buffer不够了，使用命令：
```bash
$ git config --global http.postBuffer 1048576000
$ git config --global https.postBuffer 1048576000
```
可以发现 .gitconfig 中也生成了对应的配置
```bash
$ cat .gitconfig
output:
[http]
        postBuffer = 1048576000
[https]
        postBuffer = 1048576000
```

## 3. Reference
[early EOF fatal](https://stackoverflow.com/questions/21277806/fatal-early-eof-fatal-index-pack-failed)
[hung up unexpectedly](https://stackoverflow.com/questions/38378914/how-to-fix-git-error-rpc-failed-curl-56-gnutls)
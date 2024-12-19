---
title: Linux快速查询内存占用
author: CYandYUE
date: 2024-12-19 08:33:21
index_img: /index_img/4_space.png
tags:
- Linux
- Shell
categories:
- Linux
- Shell
---

今天发现Manjaro内存爆了

自己平时也不怎么用Manjaro存东西，想着当初明明划分了300G，怎么一下子用完了，于是准备排查一下

遂记录一下怎么快速查内存占用比较方便（水一下）

## 1. Disk Free
先用df -h 看一下系统的总空间、已用空间和可用空间等信息，看看分区的问题
```bash
df -h
```
```bash
Output：

Filesystem      Size  Used Avail Use% Mounted on
......
/dev/nvme0n1p6  325G  310G   0G  100% /
......
```
发现 / 下直接挂满了，继续排查

## 2. Disk Usage

```bash
du -h --max-depth=1 /path/to/suspicious/dir | sort -rh | head -n 10
# --max-depth=1 避免递归显示所有子目录

# sort -rh : 
# -r reverse         反向排序，从大到小  
# -h human-readable  让sort够理解如 1K、2M、3G 这样的单位

# head -n 10 显示前n个
```
最终解决问题

顺便做下实验
### 1. 纯数字sort
```bash
echo "1\n2\n3" | sort -r
```
```bash
Output:
3
2
1
```

### 2. 带内存单位的sort，但不使用 -h
```bash
echo "1G\n2M\n3K" | sort -r
```
```bash
Output:
3K
2M
1G
```

### 3. 带内存单位的sort，使用 -h
```bash
echo "1G\n2M\n3K" | sort -rh
```
```bash
Output:
1G
2M
3K
```
所以要记得加 sort -h
---
title: Cudatoolkit与nvcc的关系
author: CYandYUE
index_img: /index_img/14_cuda.png
date: 2025-03-02 00:46:35
tags:
- Env
- Cuda
categories:
- Env
- Cuda
---

## 1. 问题描述
跑项目的时候发现一个很奇怪的问题

pip install -e 某个仓库的时候，其需要用cuda编译，并且指定版本是11.8

于是我就安装11.8的cudatoolkit，如下
```bash
$ conda install cudatoolkit=11.8
```
然而再次pip install -e，还是显示我的cuda版本是11.7

奇怪了，于是我查看了一下nvcc
```bash
$ which nvcc
output: /home/xxx/miniconda3/envs/xxx/bin/nvcc

$ nvcc -V
output:
nvcc: NVIDIA (R) Cuda compiler driver
Cuda compilation tools, release 11.7, V11.7.89
```
这才发现怎么toolkit是11.8，但是nvcc是11.7呢

## 2. 解决方法
查阅资料发现：

在 Conda 环境中，默认的 cudatoolkit 包并不包含 nvcc（CUDA 编译器），而是只提供运行时库。

要在 Conda 中安装指定版本的 nvcc，可以手动安装：
```bash
$ conda install nvidia/label/cuda-11.8.0::cuda-nvcc
```
不同版本的命令可以查阅[anaconda的cuda-nvcc文档](https://anaconda.org/nvidia/cuda-nvcc)

## 3. Reference
anaconda的cuda-nvcc文档: https://anaconda.org/nvidia/cuda-nvcc
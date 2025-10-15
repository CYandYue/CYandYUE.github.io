---
title: Conda env里指定nvcc
author: CYandYUE
index_img: /index_img/28_conda_nvcc.png
date: 2025-10-15 22:06:59
tags:
- Linux
categories:
- Linux
---

## 0. Motivation
今天配置环境的时候出现一个特殊情况

需要指定某个conda环境中的nvcc版本

也就是要指定cuda的位置

## 1. Method
首先可以看一下当前用的是什么版本的nvcc
```bash
which nvcc
```
如果是临时指定很简单：
```bash
conda activate env_name
export CUDA_HOME=cuda_path  # such as  /usr/local/cuda-11.1
export PATH=$CUDA_HOME/bin:$PATH
export LD_LIBRARY_PATH=$CUDA_HOME/lib64:$LD_LIBRARY_PATH
```
但是最好是写在配置文件里一直生效

首先打开conda配置文件：
```bash
conda activate env_name
vim $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
```
如果没有的话可以先创建
```bashrc
conda activate env_name
touch $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
vim $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
```
然后在配置文件里写入
```bash
# in env_vars.sh
export CUDA_HOME=cuda_path  # such as  /usr/local/cuda-11.1
export PATH=$CUDA_HOME/bin:$PATH
export LD_LIBRARY_PATH=$CUDA_HOME/lib64:$LD_LIBRARY_PATH
```
即可
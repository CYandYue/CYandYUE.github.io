---
title: 'cuda error: no kernel image is available for execution on the device'
author: CYandYUE
date: 2025-02-19 06:05:18
index_img:
tags:
- Linux
- DEBUG
- CUDA
categories:
- Linux
- DEBUG
---

## 1. 问题描述
有一个项目要用到torch，readme里的部署过程如下：
```bash
conda install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.6 -c pytorch -c conda-forge
```
但是环境配好了以后，一用到to(self.device)就会报以下的错：
```bash
runtimeerror: cuda error: no kernel image is available for execution on the device
```
以下是记录debug的过程

## 2. 排查过程
### 2.1 CUDA_LAUNCH_BLOCKING=1
报错信息中推荐将CUDA_LAUNCH_BLOCKING设置成1来debug，于是在代码头部添加如下代码：
```bash
import os
os.environ['CUDA_LAUNCH_BLOCKING=1']='1'
```
或者也可以在shell中python前加上：
```bash
CUDA_LAUNCH_BLOCKING=1 python xxx.py
```

然而，即使设置了该环境变量，也没有得到有用的信息

### 2.2 查看cudatoolkit
怀疑是cudatoolkit的版本有问题，遂查看一系列版本
```bash
import torch
print(torch.__version__)  # PyTorch 版本
print(torch.version.cuda)  # PyTorch 绑定的 CUDA 版本
print(torch.cuda.is_available())  # 检查 GPU 是否可用
print(torch.cuda.device_count())  # GPU 数量
```
经排查没有发现问题

PS: 此处说明一下torch版本和cuda版本的关系：

每个版本的Pytorch都是根据某个对应版本的cuda编译的

即使安装Pytorch时没有安装cuda，也仍然可以使用PyTorch内置的CUDA运行

具体的对应版本的安装方法可以查看[pytorch官网](https://pytorch.org/get-started/previous-versions/)

## 3. 解决方法
因为项目指定的torch和cuda版本很旧，我的显卡是4060较新

怀疑是某种不匹配

但是查阅资料发现：前例只有显卡太旧不支持新版本的cuda，报类似的错误，而没有我假设的情况

还是决定大胆假设。进行尝试：

先卸载旧版本
```bash
# 这三个是python包，既可以使用pip安装，也可以使用conda安装
pip uninstall pytorch torchvision torchaudio

# 而cudatoolkit只能使用conda安装（非python包）
conda uninstall cudatoolkit
```

再安装新版本
```bash
conda install pytorch==2.1.0 torchvision==0.16.0 torchaudio==2.1.0 pytorch-cuda=12.1 -c pytorch -c nvidia
```

经尝试竟然真的解决了问题

具体原因等时间空余后会补充

## 4. Reference
pytorch官网各版本安装文档：https://pytorch.org/get-started/previous-versions/
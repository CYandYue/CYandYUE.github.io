---
title: Linux-hugging-face
author: CYandYUE
index_img: /index_img/27_huggingface.png
date: 2025-3-10 19:40:41
tags:
- Linux
categories:
- Linux
---

## 0. Motivation
在服务器上下载hugging face权重的时候一直复制链接再wget还是太麻烦了

还是用huggingface-cli吧

## 1. Setup
首先安装一下huggingface-hub
```bash
pip install huggingface_hub
```
## 2. Terminal download
登陆huggingface-cli
```bash
huggingface-cli login
```
下载
```bash
huggingface-cli download zai-org/cogvlm2-llama3-chat-19B --local-dir /your/target/path
```

## 3. script download
```python
from huggingface_hub import hf_hub_download

hf_hub_download(repo_id="zai-org/cogvlm2-llama3-chat-19B", filename="pytorch_model.bin")
```
这将把模型权重下载到默认缓存目录，通常是 ~/.cache/huggingface/hub


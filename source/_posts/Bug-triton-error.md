---
title: cannot import name 'get_cache_invalidating_env_vars' from 'triton._C.libtriton'
author: CYandYUE
index_img:
date: 2025-03-03 21:11:27
tags:
- Linux
- DEBUG
categories:
- Linux
- DEBUG
---

## 1. 问题描述
最近要用到LLaVA-7b-v0，早期版本的LLaVA需要将llava delta weight加到base model(llama) weight上，形成checkpoint

合并的代码如下:
```bash
python3 -m llava.model.apply_delta \
    --base /path/to/llama-7b \
    --target /output/path/to/LLaVA-7B-v0 \
    --delta liuhaotian/LLaVA-7b-delta-v0
```

但是我得到了一个runtime error:
```bash
RuntimeError: Failed to import transformers.models.llama.modeling_llama because of the following error (look up to see its traceback):
cannot import name 'get_cache_invalidating_env_vars' from 'triton._C.libtriton' (/home/xxx/anaconda3/envs/xxx/lib/python3.10/site-packages/triton/_C/libtriton.so)
```

感觉是triton的版本问题，我的triton版本是2.0.0

因为triton仓库里没看到类似的issue，遂自己尝试排查

## 2. 解决方案
经过尝试，发现将triton更新到3.0.0即可解决
```bash
pip install triton==3.0.0
```

## 3. Reference
后来我自己提了个issue，详见[triton issue #6088](https://github.com/triton-lang/triton/issues/6088)
---
title: Permission to xxx denied to github-actions[bot]
author: CYandYUE
index_img:
date: 2025-03-30 23:01:49
tags:
- DEBUG
categories:
- DEBUG
---

## 1. 问题描述
最近fork了一个自动拉取arxiv论文的[仓库](https://github.com/wonderNefelibata/Awesome-LRM-Safety)

它是用Github actions的功能，配置了workflow，定时run workflow来自动拉取论文

具体的配置，即 .github/workflow/xxx.yml如下：

```bash
name: Run Arxiv Papers Daily

on:
  schedule:
    - cron: '30 2,14 * * *'  # 每天北京时间上午10点半和晚上10点半运行
  workflow_dispatch:

env:
  GITHUB_USER_NAME: xxx      # 请替换为你的 GitHub 用户名
  GITHUB_USER_EMAIL: xxx@qq.com    # 请替换为你的电子邮件地址

jobs:
  update:
    name: Update Arxiv Papers
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Set up Python Environment
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'

      - name: Install Dependencies
        run: |
          python -m pip install --upgrade pip
          pip install arxiv tenacity

      - name: Run arXiv Updater Script
        run: |
          python arxiv_updater.py

      - name: Debug File Paths
        run: |
          echo "Current working directory: $(pwd)"
          ls -la  # 列出工作目录中的文件

      - name: Check File Contents
        run: |
          echo "article.json content:"
          cat article.json | head -n 5
          echo "README.md content change:"
          git diff README.md

      - name: Commit and Push Changes
        run: |
          git config user.name "${{ env.GITHUB_USER_NAME }}"
          git config user.email "${{ env.GITHUB_USER_EMAIL }}"
          git add article.json README.md arxiv_updater.py
          git commit -m "Automatic update from GitHub Actions" || echo "No changes to commit"
          git push origin main
```

但是我自己使用类似配置的时候，run workflow会出现以下报错：
![Permission to xxx denied to github-actions[bot]](github_actions_bot.png)

## 2. 解决方案
可以发现是配置里这一段失败了
```bash
        run: |
          git add article.json README.md arxiv_updater.py
          git commit -m "Automatic update from GitHub Actions" || echo "No changes to commit"
          git push origin main
```
原因是github该仓库关于actions的设置中，bot的权限不够

解决方法是找到：

Settings -> Actions -> General -> Workflow permissions

选择Read and write permission即可

## 3. Reference
[stack overflow](https://stackoverflow.com/questions/72851548/permission-denied-to-github-actionsbot)
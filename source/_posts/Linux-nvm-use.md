---
title: nvm, npm, node知识与常用命令
author: CYandYUE
index_img: /index_img/30_nvm_npm_node.jpg
date: 2025-12-23 18:57:10
tags:
- Linux
categories:
- Linux
---

## 0. Motivation
最近经常在服务器装claude

经常接触nvm, npm, node

今天想着写一个博客记录一下我对这三个东西的理解

## 1. Overall
总的来说，我感觉nvm, npm, node 有点像 conda, pip, python的关系

node是在操作系统上运行 JavaScript 的解释器

npm是 Node Package Manager，生态的包管理器（npm install）

而nvm是 Node Version Manager，也就是版本管理器，解决的痛点是可能同时需要多个 Node 版本

是不是很像：
| Python 生态                              | Node 生态             | 作用            |
| -------------------------------------- | ------------------- | ------------- |
| `python` / `python3`                   | `node`              | 运行时/解释器       |
| `conda`（或 `pyenv`）                     | `nvm`               | 安装/切换不同版本的运行时 |
| `pip` / `conda install`                | `npm install`       | 安装第三方依赖       |
| `venv`/conda env                       | 项目本地 `node_modules` | 项目依赖隔离        |
| `requirements.txt` / `environment.yml` | `package.json`      | 声明依赖          |
| `pip freeze` / lock                    | `package-lock.json` | 锁定依赖树         |

不同点是npm是根据项目管理包，这点有点像uv

## 2. Command lines
nvm可以帮你管理node的版本
### 2.1 NVM
查看和安装
```bash
nvm --version
nvm ls                # 本机已安装版本
nvm ls-remote         # 可安装的远端版本（很多）
nvm install 18        # 安装某个大版本（18 系列）
nvm install 16.20.2   # 安装精确版本
```
切换和确认
```bash
nvm use 18
nvm use 16.20.2
nvm current           # 当前生效版本
node -v               # 确认 node 版本
npm -v                # npm 版本也会随 node 变
which node            # node 来自哪里（排错神器）
```
设置默认版本（新开终端自动用）
```bash
nvm alias default 18
nvm alias default 16.20.2
nvm alias             # 查看所有别名
```
项目级固定版本，在项目根目录创建 .nvmrc
```bash
echo "18.20.3" > .nvmrc
nvm use               # 自动读取 .nvmrc
```

### 2.2 NPM
初始化项目
```bash
npm init -y
```
安装/卸载依赖
```bash
npm install xxx           # equal to 'npm i xxx'
npm i xxx                 # 安装运行依赖（dependencies）
npm i -D xxx              # 安装开发依赖（devDependencies）
npm uninstall xxx
```

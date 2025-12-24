---
title: pnpm与npm的区别和使用方式
author: CYandYUE
index_img: /index_img/31_pnpm.jpg
date: 2025-12-24 17:19:24
tags:
- Linux
categories:
- Linux
---

## 0. Overall
pnpm（performant npm）是一个快速、节省磁盘空间的 JavaScript 包管理器。相比 npm，pnpm 采用了独特的依赖管理方式，通过硬链接和符号链接来共享依赖，避免重复安装相同的包。

## 1. Difference between pnpm and npm
- npm:
  复制机制：如果你有 10 个项目都用了 A，npm 会把 A 的代码在你的硬盘上复制 10 份。这会造成巨大的磁盘空间浪费。

- pnpm:
  全局存储 + 硬链接 (Hard Links)：pnpm 会在全局（Global Store）维护一个内容可寻址的仓库。

  当你在项目中安装 A 时，pnpm 不会复制文件，而是创建一个硬链接指向全局仓库中的 React。

  结果：无论你有多少个项目，A 在你的硬盘里只有一份。这能节省大量磁盘空间。

## 2. Use pnpm

### 2.1 安装pnpm
用npm安装pnpm
```bash
npm install -g pnpm
```
或者mac上用brew安装
```bash
brew install pnpm
```
### 2.2 使用pnpm（用slidev举例）
首先安装slidev
```bash
pnpm create slidev
```
然后某个工程文件夹里要使用slidev
```bash
cd one_folder
pnpm init               # 初始化pnpm脚本package.json
pnpm install            # 安装依赖的软连接在./node_modules 
pnpm run dev            # 跑在package.json写的脚本的名字
```
其中pacakge.json可能是这样的：
```bash
# in pacakge.json
{
  "name": "slidev-demo",
  "type": "module",
  "private": true,
  "scripts": {
    "dev": "slidev",
    "build": "slidev build",
    "export": "slidev export",
    "lecture-01": "slidev lecture-01/slides.md",
    "lecture-02": "slidev lecture-02/slides.md",
    "lecture-03": "slidev lecture-03/slides.md",
    "build-01": "slidev build lecture-01/slides.md",
    "build-02": "slidev build lecture-02/slides.md",
    "build-03": "slidev build lecture-03/slides.md",
    "export-01": "slidev export lecture-01/slides.md",
    "export-02": "slidev export lecture-02/slides.md",
    "export-03": "slidev export lecture-03/slides.md"
  },
  "dependencies": {
    "@slidev/cli": "^52.11.1",
    "@slidev/theme-default": "latest"
  }
}
```
所以想要跑lecture1的话就用：
```bash
pnpm run lecture-01
```
---
title: 'Slidev: Markdown做PPT'
author: CYandYUE
index_img: /index_img/32_slidev.jpg
date: 2026-01-04 13:54:51
tags:
- Linux
categories:
- Linux
---

## 0. Motivation
最近在寻找高效制作格式统一的ppt的方法

觉得Beamer用latex写ppt有点太繁杂了，而且编译也比较麻烦

在好友推荐下发现了Markdown做ppt的工具slidev

故写一篇博客记录一下

## 1. Why
为什么选择slidev呢，可以参考官方的[文档](https://cn.sli.dev/guide/why)

- 可交互性: slidev以Web为平台动态展示Markdown中更新的一切，无需编译或者刷新，非常方便

- 简便: 其有良好的插件，高亮，依托于Markdown也比latex更加简单，写作者能更注重内容。
在当下Vibe Coding时代，人们也能轻松的驱动Claude Code等工具来调整Markdown的内容，减少学习成本

- 社区环境：有丰富的主题

- 跨平台：支持导出为 PDF、PPTX 和图片格式，也可以通过一个简单的命令编译为静态网页，以便您分享或部署到任何地方。

## 2. Installation
推荐使用pnpm而非npm来安装slidev，原因以及pnpm安装步骤可见我之前的[博客](https://cy.terase.cn/2025/12/24/Linux-pnpm-use/)

首先用pnpm创建slidev项目
```bash
pnpm create slidev
```
你需要根据提示：
- 输入一个项目名
- 选择Install and start it now
- 在Choose the package manager时选择pnpm

这一步会：

- 根据你输入的项目名生成一个新文件夹

- 在里面放好基础文件，比如 slides.md、package.json、一些主题/配置文件

- 根据生成的package.json安装依赖

最关键的是这个初始的 package.json ，其中会写好 scripts，比如（大概长这样）：
```json
{
  "name": "slidev",
  "type": "module",
  "private": true,
  "scripts": {
    "build": "slidev build",
    "dev": "slidev --open",
    "export": "slidev export"
  },
  "dependencies": {
    "@slidev/cli": "^52.11.1",
    "@slidev/theme-default": "latest",
    "@slidev/theme-seriph": "latest",
    "vue": "^3.5.26"
  }
}
```

然后你就可以根据提示去浏览器里浏览最初的ppt效果了

## 3. Manage your package.json
现在是时候学会自己写scripts了，可以参照我的这个package.json
```json
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
简单易懂

比如我想观看lecture-03的效果我就输入
```bash
pnpm lecture-03
```

直接用pnpm加上你写的scipt alias就行

## 4. Syntax
语法这里也不细讲了，详见[官方文档](https://cn.sli.dev/guide/syntax)

这里我推荐让Claude Code帮你写，不用自己掌握语法

## 5. Transfor Pipeline
我试过用现成的ppt生成slidev，再转换回ppt

首先pip安装pptx2md
```bash
pip install pptx2md
```
用pptx2md将现场的ppt转换为中间markdown并拆出图片（语法不一定符合slidev）
```bash
pptx2md ./your_existing_pptx
```
然后prompt让Cluade Code根据中间markdown文件生成slidev格式的markdown文件即可
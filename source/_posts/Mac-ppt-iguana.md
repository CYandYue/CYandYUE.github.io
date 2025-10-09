---
title: Mac在PowerPoint里安装IguanaTex实现latex插入
author: CYandYUE
index_img: /index_img/25_iguana.png
date: 2025-10-09 14:23:47
tags:
- Mac
categories:
- Mac
---

## 0. Motivation
之前刚开始用 Mac，发现缺少一个能在 Power Point 中差入latex公式的插件

以前在 Windows 上用的是 MathType

在 Mac 似乎不行

上网查了一下发现 IguanaTex 还可以

## 1. Preliminaries
首先得保证自己已经安装了brew包管理器

可以用如下安装：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 2. Install IguanaTex
用brew安装Iguana：
```bash
brew tap tsung-ju/iguanatexmac
brew install iguanatex
```

如果出现如下提示：
```bash
"无法打开libIguanaTexHelper.dylib，因为无法验证开发者"
```
这个错误是 macOS 中的 Gatekeeper 安全特性导致的

Gatekeeper 会验证下载的应用是否来自可信的开发者

由于 IguanaTex 不是 Apple 官方认证的应用，所以可能会看到这个错误

解决该问题：
- 打开 "系统偏好设置"。
- 选择 "安全性与隐私"。
- 点击 "通用" 选项卡。
- 在 "允许从以下位置下载的应用" 部分中，选中 "任何来源"

如果发现找不到"任何来源"，这也是正常的

从macOS Sierra (10.12)开始，Mac默认隐藏了”任何来源”选项

解决方式见我的另一篇[blog](https://cy.terase.cn/2025/09/07/Mac-spctl/)

## 3. Install LaTex in Mac
这时候打开Power Point

在上面的菜单栏选中IguanaTex

会发现：
```bash
"Error while running process"
```

这是因为你的 Mac 还没有安装 LaTex 的发行版如 MacTex

### 3.1 Install MacTex
下载[MacTex](https://link.zhihu.com/?target=https%3A//www.tug.org/mactex/mactex-download.html)

## 4. Use IguanaTex
已经可以使用Iguana了

讲一些实用技巧

可以设置模版，每次添加latex公式能少写一些，提高效率

点击IguanaTex->New LaTex display

在下图中先选中 Use templates, 写入如下的代码后，选择 Save templates, 再选择 Make Default 即可
![设置模板](setup.png)

这样下次打开直接就会变成如下的模板：
![使用模板](final.png)





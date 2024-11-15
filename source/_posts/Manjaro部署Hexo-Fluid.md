---
title: Manjaro部署 Hexo+Fluid+Github Pages
date: 2024-11-15 18:03:45
tags:
- Manjaro
- 环境配置

index_img: /index_img/1_hexo.png

categories:
- 环境配置
---

记录一下在manjaro上部署Hexo，并上传到github pages的过程

## 1. Hexo安装
arch系包管理器好用，所需的nvm和hexo-cli都能直接pacman安装，如下
### 安装Git
```bash
sudo pacman -Sy git
```

### 安装Node.js
官方推荐使用nvm安装，下面先安装nvm，再安装Node.js

```bash
# installs nvm (Node Version Manager)
pacman -Sy nvm
# download and install Node.js (you may need to restart the terminal)
nvm install 22
# verifies the right Node.js version is in the environment
node -v # should print `v22.11.0`
# verifies the right npm version is in the environment
npm -v # should print `10.9.0`
```

详情可参考[官方指导](https://nodejs.org/en/download/package-manager/)

### 安装Hexo
```bash
pacman -Sy hexo-cli
```

## 2. Hexo建站
### hexo建站
```bash
hexo init <folder>
cd <folder>
hexo install
```
耗时有点久，按官方说法应该挺快的，但是我看到挺多issue提了时长问题

完成后，目录结构如下：
```bash
.
├── _config.yml     # hexo默认配置
├── package.json    # 安装的应用程序的信息
├── scaffolds       # 模板文件夹，新建文章时，会根据 scaffold 来创建文件。
├── source          # 资源文件夹
|   ├── _drafts
|   └── _posts
└── themes          # 主题文件夹
```

## 3. Fuild主题
### 安装主题 Fluid
首先安装npm，再用npm安装fuild
```bash
pacman -Sy npm
npm install --save hexo-theme-fluid
```
然后在博客目录下创建 _config.fluid.yml，将主题的 [_config.yml](https://github.com/fluid-dev/hexo-theme-fluid/blob/master/_config.yml) 内容复制进去。

### 指定主题
接着在默认配置 _config.yml 中指定主题
```yaml
theme: fluid     # 指定主题
language: zh-CN  # 指定语言，会影响主题显示的语言，按需修改
```

### 创建主题「关于页」
```bash
hexo new page about
```
完成后在 source/ 将出现 about/文件夹，用于配置「关于页」的信息

在 /source/about/index.md 中，添加 layout 属性
```yaml
---
title: about
layout: about
---

这里写关于页的正文
```

## 4. 新建Post

### Post配置
首先为了方便分别管理每篇post的图片，修改默认配置_config.yml

修改下列配置，使新建文章时，在 source/_posts/ 下生成同名文件夹，用于存放图片文件
```yaml
post_asset_folder: true # for images store
marked:
  prependRoot: true
  postAsset: true
```

### 新建Post
```bash
hexo new post <post_name>
```
出现 source/_posts/<post_name>.md 与 source/_posts/<post_name>/

前者中写文章的markdown，后者放图片资源即可

### Post图片引用
例如图片路径为 source/_posts/<post_name>/img.jpg

在正文中引用如下
```yaml
---
title: a
date: xxxx-xx-xx xx:xx:xx
tags:
- b
- c
categories:
- d
---

your post contents

![image_caption](img.jpg)
```

### Post封面图片
由于抽象原因，封面图片无法使用上述引用方法

解决办法是在 source/ 下新建一个文件夹专门存放Post封面图片

例如新建 source/index_img/

封面图片路径为 source/index_img/cover_img.jpg

引用如下
```yaml
---
title: a

# 此处第一个 / 代表根目录 source
index_img: /index_img/cover_img.jpg
date: xxxx-xx-xx xx:xx:xx
tags:
- b
- c
categories:
- d
---

```

## 5. 本地启动
```bash
hexo g   # equal to hexo generate
hexo s   # equal to hexo server
```
访问 http://localhost:4000 即可

## 6. Github Pages
### 本地git初始化
首先初始化仓库
```bash
git init
```
添加 .gitignore 如下
```yaml
/public             # 渲染结果放在public，不应该上传仓库
/node_modules       # npm install的结果，应该可以不传

db.json
package-lock.json
```
新建 .github/workdlows/pages.yml，内容如下

注意其中的 runs-on: ubuntu-latest，一开函我以为是本地的设备，写了manjaro-latest

结果github pending的时候一直在waiting device, 才反映过来写错了
```yaml
name: Pages

on:
  push:
    branches:
      - master # default branch

jobs:
  build:
    runs-on: ubuntu-latest                # 指定运行的设备
    steps:
      - uses: actions/checkout@v4
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          submodules: recursive
      - name: Use Node.js 22               # 修改成自己的版本
        uses: actions/setup-node@v4
        with:
          node-version: "22"               # 修改成自己的版本
      - name: Cache NPM dependencies
        uses: actions/cache@v4
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public
  deploy:
    needs: build
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### Github创建 .github.io
- 建立名为 username.github.io的储存库。
- 在 GitHub 仓库的设置中，导航至 Settings > Pages > Source 。 将 source 更改为 GitHub Actions，然后保存。

### 本地仓库push到 .github.io
首先在默认配置_config.yml里修改url
```yaml
url: https://<your github username>.github.io
```
```bash
git add .
git commit -m "initiation"
git remote add origin <.github.io的地址>
git push -u origin master
```

### Pending
查看 username.github.io的Action页面，可看到github pending的进程，等待完成即可

完成后会得到网址 https://\<your github username\>.github.io
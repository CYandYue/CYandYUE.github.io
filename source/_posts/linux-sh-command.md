---
title: Linux自定义Shell Command
author: CYandYUE
date: 2024-12-28 21:54:58
index_img: /index_img/8_sh_command.png
tags:
- Linux
- Shell
categories:
- Linux
- Shell
---

## 1. 问题描述
最近发现自己有一个手癖，cd 之后必须接一个 ls

因为老是忘记某个文件夹下有什么东西，得先看看

感觉这样很麻烦，于是想自定义一个命令，把 cd 和 ls 结合起来


## 2. 解决方案
### 2.1 写脚本函数
在 ~/scripts/ 下新建一个 my_functions.sh, 其中写一个函数叫做 cdl ( cd + ls )
```bash
# in ~/scripts/my_functions.sh

# for cd and ls
cdl()
{
        cd "$1" || exit 1
        ls ./
}
```
cdl的内容也很简单：cd 到第一个参数 "$1" 中，然后 ls 一下

但是这其中也有一些小细节值得注意
```bash
# 1. cd “$1" 比 cd $1 更好
# 双引号可防止 通配符globbing 和 分词splitting
# 虽然此例中不存在 globbing 的实际意义，但是养成好的习惯是好的

# 2. || exit 1 是用来防止 cd 发生错误
# false || exit 1 将执行 exit 1, 直接退出并返回退出码1
```
平时写完脚本后可以用 shellcheck检查一下，查漏补缺
```bash
$ shellcheck ~/scripts/my_functions.sh
```

### 2.2 编译函数
为了每次新开终端，都能使cdl生效，应该在 .zshrc / .bashrc 中编译函数
```bash
# in ~/.zshrc

# my own program in functions.sh
source ~/scripts/my_functions.sh
```
至此，新开一个终端，会发现 cdl 已经可以使用了
```bash
$ cdl ~/scripts
# output
my_functions.sh

$ pwd
# output
~/scripts
```

## 3. 启发
可以通过source脚本函数的方式,自定义结合任何命令，来提高平时的效率
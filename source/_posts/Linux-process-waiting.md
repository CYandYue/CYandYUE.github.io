---
title: Linux进程等待问题
author: CYandYUE
date: 2025-02-01 23:10:44
index_img: index_img/11_wait_process.png
tags:
- Linux
- Shell
categories:
- Linux
- Shell
---

## 1. 问题描述
如果我们希望等待一个进程结束之后，再开始另外一个进程，该怎么办

答案是可以使用 wait 命令，例如
```bash
$ sleep 60 & # &作用是让命令后台执行，不影响当前终端继续执行其他命令，可以实现多任务并发执行
output:
[1] 14982

$ wait 14982
# 此时这个终端就会等待进程14982 sleep 60s之后再开放
```

但是 wait 是有缺陷的，其只能对子进程生效，比如
```bash
$ sleep 60 &
output:
[1] 14982
```
此时新开一个终端，输入
```bash
$ wait 14982
output:
wait: pid 14982 is not a child of this shell
```
也就是说，wait只能查到本终端的子进程，别的终端运行的进程没法被wait找到

这种情况该怎么解决呢

答案是可以自己写个新的programme, 具体过程如下：

## 2. 利用kill的进程等待程序
### 2.1 kill 的特性
正常使用 kill 命令的时候，若其成功发送信号给进程，会返回程序码0，其他状态是非0

但是如果使用命令 kill -0, 则不会发送信号，并且在进程存在的时候返回0，不存在返回非0
### 2.2 自定义脚本函数
先创建一个脚本
```bash
$ touch my_functions.sh
$ vim my_functions.sh
```
在其中写入
```bash
# in my_functions.sh

# for wait for a process until it's finished
waitpid()
{
	# notice this while
	# when return code is 0 means True
	# it's wird, maybe refer to program code
	while kill -0 "$1"
	do
	sleep 1
	done
}
```
值得注意的是，就像上述注释中写到的：

脚本中的while + 命令的判断和常规不一样

若命令的状态码是0，相当于while的条件是True，相当于0是True，非0是False (反直觉)

### 2.3 source
为了方便可以在 .bashrc 中 source 这个脚本，每次打开终端就能直接用我们自己写的 waitpid 函数了
```bash
# in .bashrc
source path/to/my_functions.sh
```

新开一个终端
```bash
$ sleep 60 &
output:
[1] 16002
```
再新开另一个终端
```bash
waitpid 16002
```
此时可以发现，新的终端也在等待进程16002结束了，完美解决
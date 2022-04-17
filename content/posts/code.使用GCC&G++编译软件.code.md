---
title: "使用GCC/G++编译软件"
# author: 
tags:
  - C
date: '2022-04-16'
ShowToc: true
draft: false
---

描述了常见名词 GCC, G++, GDB, GNU 的含义. 并简单介绍了使用 GCC/G++ 的基本使用命令, 并且给出了一个使用命令行和 VScode 编译的例子.
<!--more-->

---

## 前置知识

- 了解编译的概念(程序码, 机器码, 链接, 预编译)
- 命令行

## 1 名词解析

- GUN - 一个开源计划, 提供了许多开源工具
- GCC - GNU Compiler Collection GNU编译器套装, 通常用于编译C, 是一个跨平台的编译器, MinGW就是基于GCC而来
- G++ - 同属于GUN, 是用于编译C++的编译器
- GDB -

## 2 安装GCC

不详细介绍, 直接安装就行, 一种可选的方法是安装 Cygwin , Cygwin 提供了一个在 Win 下开发 POSIX 系统调用的库, 以及非常全的可选工具, 其中就包括了GCC, G++, GDB.

安装成功后检查GCC是否已经包含在环境变量中, 在命令行输入 `gcc` 检查

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20211104205317.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20211104205317.png#center)

出现以上提示表示成功

## 3 编译C文件

给出一个编译器通常的编译过程作为参考

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/bg2014110803.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/bg2014110803.png#center)

给出GCC 常用的指令如下

- **c**

只激活预处理,编译,和汇编,也就是他只把程序做成obj文件

例子用法:

```
gcc -c hello.c
```

他将生成 .o 的 obj 文件

- **o**

制定目标名称, 默认的时候, gcc 编译出来的文件是 a.out

例子用法:

```
gcc -o hello.exe hello.c (哦,windows用习惯了)
　　gcc -o hello.asm -S hello.c
```

- **S**

只激活预处理和编译，就是指把文件编译成为汇编代码。

例子用法:

```
gcc -S hello.c
```

他将生成 .s 的汇编代码，你可以用文本编辑器察看。

- **E**

只激活预处理,这个不生成文件, 你需要把它重定向到一个输出文件里面。

例子用法:

```
gcc -E hello.c > pianoapan.txt
gcc -E hello.c | more
```

- **g**

在编译的时候，产生调试信息。

- **ansi**

关闭 gnu c中与 ansi c 不兼容的特性, 激活 ansi c 的专有特性（包括禁止一些 asm inline typeof 关键字, 以及 UNIX,vax 等预处理宏）。

- **C**

在预处理的时候, 不删除注释信息, 一般和-E使用, 有时候分析程序，用这个很方便的。

## 4 使用命令行编译(以GCC为例)

最简单的编译只需要输入

```powershell
gcc FILENAME.c
```

编译器会自动生成可执行文件, G++ 同理, 替换 GCC 即可

## 5 使用VScode编译

首先安装 C/C++ 相关的插件

安装完之后按着插件提示好好配置一下环境

编译可以在 `F1` 或者 `Ctrl+Shift+P` 窗口中搜索 `task` 之后选择 GCC 或者 G++ 编译即可.

## 参考

1. [https://www.runoob.com/w3cnote/gcc-parameter-detail.html](https://www.runoob.com/w3cnote/gcc-parameter-detail.html)
---
title: "编译C文件到汇编语言"
# author: 
tags:
  - C
  - 汇编
date: '2022-04-16'
ShowToc: true
draft: true
---

用 GCC 编译 `.c` 文件到汇编语言, 便于汇编语言的学习
<!--more-->

---

## 前置知识

- VSC 配置文件编写
- GCC

## 在VSC中配置GCC编译选项

在VSC中按 `F1` 进入GCC的任务配置, 添加以下配置, 只要参考args那个部分就可以了, 其他根据当前环境各有不同.

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "type": "cppbuild",
      "label": "C/C++: gcc.exe 生成活动文件",
      "command": "C:\\cygwin\\bin\\gcc.exe",
      "args": [
        "-S",
        "-o",
        "${workspaceFolder}/out.s",
        "${file}"
      ],
      "options": {
        "cwd": "${fileDirname}"
      },
      "problemMatcher": [
        "$gcc"
      ],
      "group": "build",
      "detail": "编译器: C:\\cygwin\\bin\\gcc.exe"
    },
  ]
}
```

## 参考

1. [http://beanocean.github.io/tech/2013/10/09/generate_assembler_from_c_code/](http://beanocean.github.io/tech/2013/10/09/generate_assembler_from_c_code/)
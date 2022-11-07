---
title: "使用requirements文件快速安装/导出开发环境"
# author: 
tags:
  - Python
date: '2022-04-16'
ShowToc: true
draft: false
---

通过 `requirements.txt` 文件快速安装和导出python环境的方法
<!--more-->

---

## 前置知识

- pip基本使用方法


## 1 安装

在工作目录下控制台输入

```bash
pip install -r requirements.txt
```

## 2 导出

要导出 `requirement.txt` 依赖文件, 最好借助 `pipreqs`

在需要导出的目录下控制台输入

```bash
pip install pipreqs # 安装pipreqs
pipreqs ./
```

## 问题补充
1. 报错 `'gbk' codec can't decode byte 0xb0 in position 772: illegal multibyte sequence`
换成
```shell
pipreqs ./ --encoding=utf8
```

## 参考

无
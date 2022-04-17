---
title: "使用Anaconda管理Python环境"
# author: 
tags:
  - Python
date: '2022-04-16'
ShowToc: true
draft: false
---

使用Conda更方便得管理Python环境
<!--more-->

---


## 1 **创建环境**

```powershell
conda create -n NAME python=3.9
```

## 2 **删除环境**

```powershell
conda remove -n NAME --all
```

## 3 **激活环境**

```powershell
//激活某个环境
conda activate NAME
//返回base环境
conda activate
```

## 4 验证环境

```powershell
conda info --envs
```

## 5 管理Package

```powershell
/*1.先激活要搜索的环境,然后检查 Anaconda 存储库中是否有尚未安装的名为“beautifulsoup4”的包*/

conda search beautifulsoup4

/*2.Conda 在 Anaconda 存储库中显示具有该名称的所有包的列表，因此我们知道它可用。*/

conda install beautifulsoup4

/*3.查看新安装的程序是否在这个环境中：*/

conda list
```

## 参考

1. [https://blog.csdn.net/H_O_W_E/article/details/77370456](https://blog.csdn.net/H_O_W_E/article/details/77370456)
2. [https://conda.io/projects/conda/en/latest/user-guide/getting-started.html](https://conda.io/projects/conda/en/latest/user-guide/getting-started.html)
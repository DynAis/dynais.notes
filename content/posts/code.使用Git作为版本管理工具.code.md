---
title: "使用Git作为版本管理工具"
# author: 
tags:
  - Git
date: '2022-04-16'
ShowToc: true
draft: false
---

介绍了Git作为版本管理工具的一些基本概念和在控制台下常见指令的使用方法, 因为GUI界面下的操作很直观所以并没有费力介绍.
<!--more-->

---

## 前置知识

- 控制台的使用方法
- 基本命令行知识

## 1 Git基本概念介绍

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/202204162209607.png#center)


### 1.1 仓库

Git中, 仓库(Repository)指的是当前的工作区, 通常即为工作文件夹, 一个仓库是一切后续操作的起点, 一个项目通常对应一个仓库

### 1.2 分支

Git中, 分支(Branch)指的是相对于主干(Master)来说的其他"分支版本". 

在最一般的情况下, 我们只需要一条主干即可完成项目的版本管理, 不需要分支, 如果把所有的版本根据时间线视觉化, 则如一条直线一般.

![Untitled](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/Untitled%201.png#center)

但在长时间的长久开发中, 有时也许会有新的点子需要大幅改动原有项目或者原有风格, 此时如果仍然在主干中继续开发就非常不妥, 此时就需要分支功能

分支就犹如一条变动的世界线, 从原有的世界线上分离出来, 并在将来的某一个时间点, 又会收束回到原有的世界线上去, 一个分支直观的可以展示为下图紫色线条的样子

![Untitled](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/Untitled%202.png#center)

其中版本v3.0.X基于版本v3.0.0产生了新的分支, 并且在v4.0.X之后合并回了主干中

既使用分支可以在不干扰基础功能的情况下开发新的功能

### 1.3 版本库

工作区有一个隐藏目录 .git，这个不算工作区，而是 Git 的版本库

版本库中保存着所有更改的历史记录

## 2 Git的常见使用场景和命令

下面这张图直观的展现了Git的常用命令是如何影响工作空间的

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210820002249.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210820002249.png#center)

### 2.1 基本操作

- `git config`
  
    *设置个人信息和文本编辑器之类的首选项*
    
    ```bash
    git config --global user.name "DynAis"
    git config --global user.email dynais2499@gmail.com
    ```
    
- `git status`
  
    *查看当前待提交状态*
    
- `git diff [source_branch target_branch]`
  
    *Show changes between commits, commit and working tree, etc*
    
    ```bash
    git diff [file] # 显示暂存区和工作区的差异
    git diff HEAD # 查看已缓存的与未缓存的所有改动
    git diff [first-branch]...[second-branch] # 显示两次提交之间的差异
    ```
    
- `git log`
  
    *查看提交历史*
    

### 2.2 建立仓库

- `git init`
  
    *在当前目录下建立一个新的仓库*
    
- `git clone [url]`
  
    *克隆一个仓库*
    
- `git pull origin`
  
    *从远程获取代码并合并本地的版本*
    

### 2.3 提交更改

- `git add *`
  
    *添加所有未被加入的文件进入缓冲区*
    
- `git commit -m "Message"`
  
    *提交更改并且附上Message*
    

### 2.4 分支

- `git branch`
  
    *显示当前分支或者使用 `git push origen [branch]` 来创建分支*
    

### 2.5 发布

- `git tag`
- `git push origen [branch]`

### 2.6 回滚/合并

- `git checkout [hash] [branch]`
  
    *回滚版本*  
    
- `git merge`

## 参考

1. [https://www.runoob.com/git/git-tutorial.html](https://www.runoob.com/git/git-tutorial.html)
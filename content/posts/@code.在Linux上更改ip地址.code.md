---
title: "在Linux上更改ip地址"
# author: 
tags:
  - Linux
date: '2022-07-11'
ShowToc: true
draft: true
---
在Linux上更改ip地址
<!--more-->

---

## 前置知识

- 无

## 命令行
``` bash
sudo ifconfig eth0 172.18.128.143 netmask 255.255.255.0 broadcast 172.18.128.255 
sudo route add default gw 172.18.128.1
```

## 参考
- https://blog.csdn.net/liukun321/article/details/6662950
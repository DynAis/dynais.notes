---
title: "采样定理"
# author: 
tags:
  - 信号与系统
date: '2022-04-16'
ShowToc: true
draft: false
---
一些Nyquist采样定理与香农采样定理
<!--more-->

---


## 前置知识
- 信号与系统

## Nyquist采样定理
Nyquist采样定理指出, 采样信号的频率必须高于被采样信号最高频率的两倍，才可以避免混叠现象. 既:
$$
f_a > 2f_{g}~(a:abtastung, g:grenz)
$$

## 香农采样定理(带通采样定理)
对于带通信号采样频率只需大于信号带宽的两倍
$$
f_a > 2B~(a:abtastung, B:Bandbreit)
$$
为什么要用带通采样定理呢？按理说，奈奎斯特采样定理不是通吃一切吗？话虽如此，奈奎斯特说，只要采样率不小于信号最高频率的2倍，采样后的信号就能能够准确恢复。

可事实上，有很多行不通的地方，并不是说理论行不通，而是器件做不到，对于频带信号（带通信号）而言，例如天线发出的信号以及接收的信号，可以说都是频带信号，因为频带信号便于传输，这些信号的频率随着时代的进步，也越来越大，电磁信号向着GHz甚至数十GHz发展，如果再用奈奎斯特采样定理采样，如此之高的采样率ADC恐怕难以做到吧。

## 参考

1. [https://blog.csdn.net/Reborn_Lee/article/details/81975499](https://blog.csdn.net/Reborn_Lee/article/details/81975499)
2. https://zh.wikipedia.org/wiki/%E9%87%87%E6%A0%B7%E5%AE%9A%E7%90%86
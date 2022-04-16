---
title: '[CV] Sobel算子'
tags:
  - OpenCV
date: 2020-02-15
---



### 相关API

```c++
Sobel();//索贝尔算子
Scharr();//Sobel的加强
```



### 笔记

- **Sobel:** [边缘检测算法及各自的优缺点](https://www.jianshu.com/p/2a06c68f6c14)

  Sobel是离散的一阶微分算子,可以用来计算图像的梯度(一阶), 常用于得到图像的边缘特征, 除了Sobel之外还有其他的算子, Sobel的优势是速度比较快, 但是在准确度上有欠缺



- **使用加减来简化计算机的负担:** [sobel算子的原理与实现](https://blog.csdn.net/qq_37124237/article/details/82183177)

  乘除对计算机很费力, 对计算机应该采用近似计算, 在Sobel求边缘的合成阶段使用到了这种思想



- **整个流程:**

   高斯->转灰度->求梯度x与y->混合
   
   <!-- more -->

### 源

```c++
无
```


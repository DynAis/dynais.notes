---
title: 线性回归模型
tags:
  - Machine Learning
date: 2021-02-21
draft: true
---

线性回归是回归问题中的一种，线性回归假设目标值与特征之间线性相关，即满足一个多元一次方程。
<!--more-->

---

通过构建损失函数，来求解损失函数最小时的参数 $w$ 和$b$。通常我们可以表达成如下公式：
$$
\hat{y} = wX + b 
$$
$\hat{y}$ 为预测值，自变量 $x$ 和因变量 $y$ 是已知的，而我们想实现的是预测新增一个 $x$ ，其对应的 $y$ 是多少。因此，为了构建这个函数关系，目标是通过已知数据点，求解线性模型中 $w$ 和 $b$ 两个参数。

## 1.线性回归概述
---
线性回归是回归问题中的一种，线性回归假设目标值与特征之间线性相关，即满足一个多元一次方程。通过构建损失函数，来求解损失函数最小时的参数 $w$ 和$b$。通常我们可以表达成如下公式：

$$
\hat{y} = wX + b \tag{1}
$$

$\hat{y}$ 为预测值，自变量 $x$ 和因变量 $y$ 是已知的，而我们想实现的是预测新增一个 $x$ ，其对应的 $y$ 是多少。因此，为了构建这个函数关系，目标是通过已知数据点，求解线性模型中 $w$ 和 $b$ 两个参数。

为此, 线性回归分为两个部分, 向前传播和向后传播, 向前传播负责验证当前参数下对数据的拟合程度, 而向后传播通过在向前传播内得到的数据对参数进行优化

## 2.向前传播

### 2.1.进行数据预处理

拟合数据之前, 需要对数据先进行预处理

#### 参数初始化

参数 $w$ 和 $b$ 对初始化没有特别的需求, 置 $0$ 即可

#### 特征缩放/均一化

对于输入特征值矩阵 $X$ 中数据规模差距大的时候, 应该事先对数据进行特征缩放, 此举的目的是为了在计算中使梯度更快的收敛

### 2.2.计算预测结果及损失函数

求解最佳参数，需要一个标准来对结果进行衡量，为此我们需要定量化一个目标函数式，使得计算机可以在求解过程中不断地优化。

针对任何模型求解问题，都是最终都是可以得到一组预测值 $\hat{y}$ ，对比已有的真实值 $y$ ，数据行数为 $m$ ，可以将损失函数定义如下：
$$
J = \frac{1}{m}\sum_{i=1}^{m}{(\hat{y_i} - y_i)^2} \tag{2}
$$
值 $J$ 就代表着当前模型和数据点的偏移程度

## 3.向后传播

### 3.1.梯度下降

计算出损失函数之后, 通过使用原有参数减去一个常数与函数求导结果相乘的方式就可以不断地减小损失函数的值, 使参数不断收敛到最佳值, 这种方法在数学上也被称为**最小二乘法**, 在这里我们称为**梯度下降**:

$$
w := w - \alpha \cdot dw    \tag{3}
$$
$$
d := d - \alpha \cdot dw  \tag{4} 
$$

### 3.2.学习速率α

梯度下降算法的每次迭代受到学习率影响, 如果 **$\alpha$ 过小**, 则**达到收敛所需的迭代次数会非常高**; 如果学习率 **$\alpha$ 过大**,每次迭代可能不会减小价函数, 可能越局部最大, 导致**无法收敛**

使用时可以从小到大成倍增加尝试, 如 $0.01, 0.02, 0.04 ...$

## 4.拓展-多项式回归

有时候, 预测结果与输入值之间的关系**并非是线性**的, 此时就需要使用**多项式回归**进行拟合

比如一个二次方模型:
$$
\hat{y} = w_1 x_1 + w_2 x_2^2 + d \tag{5}
$$
此时可以使
$$
x_2 = x^2 \tag{6}
$$
来转化问题成为一个线性回归问题

## 5.拓展-正规方程

---

通过正规方程可以直接解出向量 $w$, 这种方法适用于样本量不大的情况
$$
w = (X^T X)^{-1} X^T Y \tag{7}
$$

## 参考
- [机器学习 | 算法笔记- 线性回归（Linear Regression）](tps://www.cnblogs.com/geo-will/p/10468253.html)

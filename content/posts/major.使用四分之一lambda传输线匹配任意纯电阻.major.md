---
title: "使用四分之一lambda传输线匹配任意纯电阻"
# author: 
tags:
  - 高频电路
date: '2022-04-17'
ShowToc: true
draft: false
---
使用四分之一$\lambda$长的传输线具有匹配任意纯电阻元件的能力
<!--more-->

---

## 前置知识
- 史密斯图
- 传输线理论
- 电磁场

## 原理
信号经过四分之一$\lambda$长的传输线, 在史密斯图上就可以看出, 刚好是旋转了180度
![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/202204170011046.png?x-oss-process=image/format,jpg/interlace,1#center)
由此可以借由调整传输线的$R_L$, 既特性阻抗, 达到使传输线两段(负载及前段传输线)匹配的效果, 注意只对纯电阻匹配有效.

## 匹配
对于以下给出的这种问题:
![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/202204170014763.png#center)
给出一个$200\Omega$ 的负载以及$50\Omega$的前段传输线, 现在要求使用一根四分之一$\lambda$长的传输线使前后阻抗匹配.
使用公式:
$$
R_{L}= \sqrt{{R_{Start}}\cdot{R_{Ziel}}}
$$
![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/202204170007056.png#center)


## 参考
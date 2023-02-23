---
title: "以ControlNet为基础实现设计快速迭代的可能性探索"
# author: 
tags:
 - stable ddiffusion
 - ai
 - control net
 - design
 - garment design
 - garment develop
date: '2023-02-23'
ShowToc: true
draft: true
---

<!--more-->

---

## Required knowledge

## 1 ControlNet的特点及其相关使用技巧

### 1.1 模型选择

#### dalcefo_v3_anime_pastelMix

![](Pasted%20image%2020230223225307.png)
```
dalcefo_v3_anime_pastelMix 使用指南:

trigger words needs not.

strongly recommand use prompt "flat color" with "coloful"

also recommand hires.fix with denoising strength 0.5~0.7.

if you have some problem with this model, pleas check "Use old karras scheduler sigmas (0.1 to 10)" on settings.
```

#### dalcefo_v3_painting

![](Pasted%20image%2020230223225335.png)
```
dalcefo_v3_painting 使用指南:

trigger word is "dalcefo" but it might needs not.

strongly recommand "realistic" prompt

without the prompt "realistic" generate anime style.

also recommand hires.fix with denoising strength 0.5~0.6.

if you have some problem with this model, pleas check "Use old karras scheduler sigmas (0.1 to 10)" on settings.
```

#### MIX-Pro-V3
![](Pasted%20image%2020230223225947.png)
```
MIX-Pro-V3 使用指南:

All sample images did not using highrexfix
```

#### Easynegative



### 1.2 常用tag
```
flat color, 1girl, solo, {{white background}}, standing, full body, illustration, {{simple background}}, extremely detailed CG

EasyNegative
```

## 2 实用性测试

### 2.1 场景一: 根据关键词生产设计灵感

### 2.2 场景二: 根据配色生产设计灵感

### 2.3 场景三: 根据已有线稿生产服装细节

### 2.4 场景四: 设计变异

### 2.5 场景五: 配色变异

### 2.6 场景六: 基于设计图打光/AO

### 2.7 场景七: 基于贴图打光/AO

### 2.8 场景八: 基于渲染图打光/AO

## 3 总结

## References
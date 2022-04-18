---
title: "UDIM,是什么以及怎么做"
# author: 
tags:
  - Blender
  - SP
  - UDIM
date: '2022-04-18'
ShowToc: true
draft: true
---
A templet for quick generate content.
<!--more-->

---

## 前置知识
- Blender
- SP
- UV基础

## Draft
- UDIM只是一种UV偏移
- 孤岛不能跨分区
- UDIM是一种更灵活的方式去增加分辨率， 可以自行分配给需要高分辨率的区域更多的UDIM分区
- UDIM可以把很多图像当成一个图像一起处理
- blender - rizomuv - sp
- 可以在sp单独开关和遮蔽udim分区（但好像实际上还是画在上面了的？）
- 在sp中， 选中单独分区可以单独调整分辨率
- 在遮蔽模式下左键开关遮蔽
- 使用文件夹当作大mask
- 导入时只要选择第一个udim就可以导入整个序列

## 参考
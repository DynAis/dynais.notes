---
title: "详解ParentConstraint"
# author: 
tags:
  - Unit
date: '2022-05-12'
ShowToc: true
draft: true
---
ParentConstraint到底是什么?
<!--more-->

---

## 前置知识

## 1 问题
- 和直接放入Hierarchy下有什么区别
	- 不影响比例
	- 可以连接多个父对象
- 为什么会发生位置变换(坐标到底如何计算)
	- 只得向会继承父对象的旋转和平移。旋转的轴心为负对向的原点。
	- 单机active时会记录保存当前游戏对象的offset信息。(先拖入副对象，再点active。)
	- 请注意，Inspector 中任何子游戏对象的 Transform 值都是相对于父项 Transform 值显示的结果。这些值称为__局部坐标__。
	- 在设置变换组件的父子关系时，一种有用的做法是在添加子项之前将父项的位置设置为 <0,0,0>。这意味着子项的局部坐标将与全局坐标相同，因此更容易确保子项处于正确位置。

## 2 Temp

## 参考
- https://docs.unity3d.com/Manual/class-ParentConstraint.html
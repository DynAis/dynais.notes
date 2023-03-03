---
title: "How did you find here?"
# author: 
tags:
  - TEMPLET
date: '2023-03-03'
ShowToc: true
draft: true
---
A template for quickly generating content.
<!--more-->

---

## Required knowledge

## 1

## 表格

| 属性                  | 功能                                                  |
| :--------------------------- | :----------------------------------------------------------- |
| **Stretching Stiffness**     | 布料的拉伸刚度。                                             |
| **Bending Stiffness**        | 布料的弯曲刚度。                                             |
| **Use Tethers**              | 施加约束以帮助防止移动的布料粒子离开固定粒子的距离太远。此属性有助于减少过度拉伸。 |
| **Use Gravity**              | 是否应该对布料施加重力加速度？                               |
| **Damping**                  | 运动阻尼系数。                                               |
| **External Acceleration**    | 施加在布料上的恒定外部加速度。                               |
| **Random Acceleration**      | 施加在布料上的随机外部加速度。                               |
| **World Velocity Scale**     | 角色多大程度的世界空间移动会影响布料顶点。                   |
| **World Acceleration Scale** | 角色多大的世界空间加速度会影响布料顶点。                     |
| **Friction**                 | 布料与角色碰撞时的摩擦力。                                   |
| **Collision Mass Scale**     | 碰撞粒子的质量增加量。                                       |
| **Use Continuous Collision** | 启用连续碰撞来提高碰撞稳定性。                               |
| **Use Virtual Particles**    | 每个三角形添加一个虚拟粒子，从而提高碰撞稳定性。             |
| **Solver Frequency**         | 解算器每秒迭代次数。                                         |
| **Sleep Threshold**          | 布料的睡眠阈值。                                             |
| **Capsule Colliders**        | 应与此 Cloth 实例碰撞的 CapsuleCollider 的数组。             |
| **Sphere Colliders**         | 应与此 Cloth 实例碰撞的 ClothSphereColliderPairs 的数组。    |

## 风模拟
![](Pasted%20image%2020230303141143.png)
对Y施加动画
{GIF动画演示}

## 防止移动时穿模
![](Pasted%20image%2020230303142047.png)

## 性能
无
![](Pasted%20image%2020230303143134.png)
LOD3
![](Pasted%20image%2020230303143207.png)
LOD2
![](Pasted%20image%2020230303143254.png)
## References
- [Unity Documents: Cloth](https://docs.unity3d.com/Manual/class-Cloth.html)
- [Cloth Physics Tutorial Unity 2019.4.31](https://www.youtube.com/watch?v=x91OyRjruxo)
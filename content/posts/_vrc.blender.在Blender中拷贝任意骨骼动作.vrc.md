---
title: "在Blender中拷贝任意骨骼动作"
# author: 
tags:
  - Blender
date: '2022-04-17'
ShowToc: true
draft: true
---
拷贝任意来源的人物动作(如Mixamo, MMD)作为自己的资产使用. 原理使用了骨骼限定修改器.

使用了****BoneAnimCopy****来加速工作流程. 同时写出了一些使用时应该注意的问题
<!--more-->

---

## 注意! 
**本文暂时为自己存档记录使用, 所以文章中会出现只有我自己有的文件, 因为我的模型骨骼系统不太一样有些麻烦, 直接查看最底下的参考即可, 视频说的很清晰, 以后可能考虑研究一篇转换任意动作到VRC人物上的文章(估计得等我人物做完, 遥遥无期)**

## 前置知识

- Blender 骨骼系统
- Blender 动画系统

## 1 如何使用(以Mixamo为例)

**注意!** 例子使用的是基于 **universal_human_body** 的骨骼系统, 这套骨骼绑定的很好操控也很方便, 但是很难直接映射到这个系统上来, 所以对骨骼进行了非常多的修改, 保存了一个文件, 下次使用的时候建议直接根据文件修改. 但其实修改的版本以为也是第一次做有很多不完善的地方, 只能说是强行跑起来了, 以后有空可以再优化一下. 应该不会写修改过程, 太麻烦了.

同时这套流程没有映射手指和手掌的动作, 因为一直映射不对

打开修改过的基础身体

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206204036820.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206204036820.png?x-oss-process=image/format,jpg/interlace,1#center)

在Mixamo导出FBX动作文件, 导入Blender, 导入时记得勾选**自动骨骼坐标系**, 不然骨骼的指向很奇怪

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206163034095.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206163034095.png?x-oss-process=image/format,jpg/interlace,1#center)

导入之后就可以打开插件匹配骨骼了

首先确认**手和脚的骨骼处于FK状态**

 

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206204928018.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206204928018.png?x-oss-process=image/format,jpg/interlace,1#center)

匹配骨骼的过程非常繁琐, 这次直接做了预设, 选择即可

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206203207923.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206203207923.png?x-oss-process=image/format,jpg/interlace,1#center)

然后还有些需要修正的地方

打开自己骨骼的姿态模式, 修改 **Pelvis** 或者是 **PelvisBone** 的**Z轴向映射为翻转**

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206204214549.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206204214549.png?x-oss-process=image/format,jpg/interlace,1#center)

最后确认一下有没有问题, 动作大致一样的话建议别折腾了

如果**人物双脚没有踩在地面**上的话**调整一下参考骨骼的缩放**

完事, 插件还可以直接烘焙动画.

## 2 原理

看参考里的视频吧, 不想写了

## 3 遇到的问题 / 应该注意的点

### 骨骼轴向不对

常见问题, 尝试调整插件里的骨骼旋转和骨骼约束里面的镜像

### 骨骼自己旋转

折磨, 首先检查骨骼本身有没有其他的限制器或者控制器, 是在找不出问题建议重开, 有时候莫名其妙就好了.

### 明明映射了骨骼但是旋转还是不一样

检查 IK FK, 检查控制器.

## 4 补充-MMD的映射

又做了MMD的映射, 但是MMD的腰部太奇怪了, 映射老坏, 只能说选取一小段还是可以的, 下面是导入MMD的设置

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220208001542524.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220208001542524.png?x-oss-process=image/format,jpg/interlace,1#center)

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220208001702445.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220208001702445.png?x-oss-process=image/format,jpg/interlace,1#center)

## 参考

1. https://github.com/kumopult/blender_BoneAnimCopy
2. [https://www.bilibili.com/medialist/play/watchlater/BV1Bf4y1q7aQ](https://www.bilibili.com/medialist/play/watchlater/BV1Bf4y1q7aQ)
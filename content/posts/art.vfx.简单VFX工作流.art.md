---
title: "简单VFX工作流"
# author: 
tags:
  - VFX
  - ACES
date: '2022-04-17'
ShowToc: true
draft: false
---
自己摸索出来的简单VFX所需要的全部流程. 基于ACES工作流. 以一个小项目作为案例讲解.
<!--more-->

---

**SAMPLE(befor VS after):**

![befor](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/moon_src.png#center)

![after](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/moon.png#center)

## 前置知识

- 了解ACES
- Blender
- 达芬奇
- 合成

## 1 前期

### 1.1 规划选题

在前期规划中, 建议对制作的难度有一个大概的预估. **环境光的复杂程度**, **前后的遮挡关系**, **相机的移动程度**, **模型的复杂程度**, **特效的制作难度**这些都需要有一个大概的预估, 如果没有做好选题贸然拍摄, 很有可能就会因为技术不够或者环境太难匹配造成结果不真实甚至只能半途而废.

### 1.2 正式拍摄

#### 1.2.1 HDRI

**HDRI全景图**在渲染结果的真实度提升上非常有帮助, 最理想的情况下就是借助360度的相机记录环境光的信息, 比如最常见的insta360.

如果没有360度相机, 无法记录现场的环境光信息, 那么在前期的规划中就应该已经料想到这一点并且**避免光照过于复杂的场景**. 而应该选择**光源相对单一且常见的场景**, 比如开阔的空地.

在示例项目中我只使用了手机进行拍摄, 所以选择了阴天的草地这种简单的场景, 这样使用网上众多的开源HDRI也可以实现相似的效果从而避免不真实的渲染.

#### 1.2.2 环境模型

**间接光**是增加渲染真实度的重要元素之一, 在这方面除了HDRI给出的光信息之外, 一个**现场环境的大致模型**也是相对必要的. 手工建模当然是一种方法, 但是为了节省时间可以选择通过3维扫描的方式快速还原现场的大致样貌. 这方面使用新款 IPhone 或者 IPad 的 LiDAR 最方便, 也可以选择使用相机拍摄后通过 Mashroom 合成.

#### 1.2.3 拍摄手法

考虑到后期的追踪精度问题, 对于拍摄手法的选择也是有必要的, 一般来说, **越稳定的拍摄手法**以及**越少的视角移动**肯定是会大大降低后期的难度的.

除此之外, 最好应该人为设定**曝光和白平衡保持不变**, 不然非常不利于后期进行处理.

#### 1.2.4 坐标平面参考与色彩校准

如果是**静帧合成**, 也就是只有一张图片的话, 在前期拍摄的时候多拍一张用于相机求反的照片也是很好地选择, 特别是在照片本身缺少坐标参考的情况下. 这里指的就是**通过人为的方法创造一些能够进行XY平面参考的直线对象**, 方便后期进行XY平面的对齐.

以这次的实例工程为例, 由于我前期缺乏考虑, 拍摄的地面又非常空旷没有人造物参考, 造成我在进行相机求反的时候很难校准, 增添了很多不必要的工作量.

此外, 如果有条件最好可以同时进行色彩和白平衡的校准. 当然由于经费的问题指定是不太可能的了.

#### 1.2.5 录制设置

由于这次使用的是ACES流程, 在后期时需要进行一个IDT转换, 所以录像设置也关系到转换效果的好坏. 最理想的情况下应该进行 **RAW 格式**或者 **log 格式**的记录, 比如 **Sony Raw** 或者 **Slog**. 这样可以的到最好的转换效果, 设备不支持的话则只能进行有损失的转换.

此外, 也应该注意录制时**帧率的统一**, **24帧**是比较合理的选择, 毕竟后期渲染起来更省力.

一切准备完之后就可以进行正式的拍摄了.

## 2 后期

### 2.1 建立ACES工作流

#### 2.1.1 在达芬奇中转换片段到ACES

在项目设置中的色彩管理处**设置色彩科学为 ACEScc**, **输入设备转换设置为相应的 RAW 或者 log 格式**, 不支持 RAW 等格式的机器(比如手机)则选择 sRGB, **输出设备转换为sRGB**.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912221455.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912221455.png#center)

之后就可以进行视频片段的**初次白平衡, 曝光以及色彩校准**. 这一次校准的目的**是为了还原现场场景而非添加色调**.

在交付面板中, 更改输出格式如下, 注意一定需要选取 **EXR** 格式.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912221730.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912221730.png#center)

校准完毕后, 输出之前需要**重新更改输出设备转换为无**, 不然输出的画面会是 sRGB 的色彩空间

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912221840.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912221840.png#center)

#### 2.1.2 在Blender中建立ACES环境

在目前的版本中 Blender 并没有自带 ACES OCIO, 需要下载 ACES 的分支版本或者手动进行安装. 安装完成后就可以在**渲染设置中选择 ACES 色彩空间**. 此外, 序列编辑器的色彩空间也应该改为 **ACEScg**.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222146.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222146.png#center)

**使输出设置与视频片段应该保持一致**.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912225751.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912225751.png#center)

输出选项中设置输出文件格式为**OpenEXR MultiLayer**.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912225823.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912225823.png#center)

确保渲染引擎使用**Cycles**.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222051.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222051.png#center)

**打开渲染设置中胶片选项的透明**，使输出结果的背景保持透明, 方便后期合成.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222254.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222254.png#center)

另外很重要的一点就是应该**对不同的主体区分不同的集合**, 如这次的地面与主体就分别为两个集合, 这样在集合设置中就可以针对不同的集合开启排除选项, 使得物体阴影单独渲染. 一般分物体和地面两个集合即可.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222457.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222457.png#center)

**创建两层图层, obj 和 shadow**, 分层单独渲染物体和影子.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222604.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222604.png#center)

选中 obj 图层后, **对地面集合开启进间接选项**以排除地面, 但会保留间接光的影响.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222635.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222635.png#center)

**切换为 shadow 图层对 obj 集合进行同样的操作**, 除此之外记得开启地面的**阴影捕捉**选项, 让地面只渲染阴影.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222713.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912222713.png#center)

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912223416.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912223416.png#center)

### 2.2 静帧3D特效

#### 2.2.1 使用fSpy相机求反

处理完之后通过插件导入Blender

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912225419.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912225419.png#center)

### 2.3 视频片段3D特效

#### 2.3.1 运动解算

这部分参考 CG Geek 的这个视频

{{< youtube BYH5pDYakk >}}
[https://www.youtube.com/watch?v=-BYH5pDYakk](https://www.youtube.com/watch?v=-BYH5pDYakk)

### 2.4 输出与合成

#### 2.4.1 分层输出

在匹配完场景后输出选项内开启这些比较常用的通道, 方便后期合成, 追求更高精度的话甚至可以开启Cryptomatte, 就可以选取甚至包含景深的物体了, 但是因为是简单模式这部分就不接触了.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912230008.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912230008.png#center)

#### 2.4.2 合成与后期

这里只放一张演示项目的 Compositing 面板节点, 直接在 Blender 内处理最方便, 也可以选择 Nuke 等专业软件.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912230217.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210912230217.png#center)

## 3 DLC

使用IPAD直接对影片进行摄像机追踪, 不需要相机求反了!

也可以用这个来做真实的相机移动

[https://www.youtube.com/watch?v=qgWMjCgPywo](https://www.youtube.com/watch?v=qgWMjCgPywo)
{{< youtube qgWMjCgPywo >}}

## 参考

1. [https://www.youtube.com/watch?v=aJF2sAjRsy0](https://www.youtube.com/watch?v=aJF2sAjRsy0)
2. [https://www.youtube.com/watch?v=-BYH5pDYakk](https://www.youtube.com/watch?v=-BYH5pDYakk)
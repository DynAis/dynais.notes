---
title: "线稿提取"
# author: 
tags:
  - PS
date: '2022-04-17'
ShowToc: true
draft: false
---
提供了一种通过图像处理的手段提取线条清晰的图片线稿的思路.
<!--more-->

--
**演示:**

![befor](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913115615.png?x-oss-process=image/format,jpg/interlace,1#center)


![after](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913115700.png?x-oss-process=image/format,jpg/interlace,1#center)

# 前置知识
- PS
- 图像处理

# 1 源图像需求

原图像要求线条清晰, 并且颜色应当深于内部颜色, 考虑到后续的侵蚀操作, 图像分辨率越高提取的效果越好.

# 2 线稿提取

提取线稿分为五步, **去色 反向 叠加 侵蚀 调整,** 通过原图像在反向后使用线性减淡(添加)(既加法模式)会变为白色这一特点, 配合侵蚀操作消除反向后的线条从而保留线稿的思路完成.

### 去色

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913120415.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913120415.png?x-oss-process=image/format,jpg/interlace,1#center)

### 反向

拷贝一份新的图层, 在Photoshop中使用 `ctrl + i` 即可快速反向, 得到反向图层.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913120707.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913120707.png?x-oss-process=image/format,jpg/interlace,1#center)

### 叠加

更改反向后的图层混合模式为线性减淡(添加), 也就是加法模式, 如果操作正确这是画面应该为全白. 图层顺序为反向图层在上未反向图层在下.

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913120944.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913120944.png?x-oss-process=image/format,jpg/interlace,1#center)

### 侵蚀

对反向图层使用 `滤镜 - 其他 - 最小值` 这是PS中的侵蚀操作, 更改半径到合适大小, 到这一步可以提取出大致的线稿, 但还有一些杂乱暗淡的线条. 

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913120744.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913120744.png?x-oss-process=image/format,jpg/interlace,1#center)

### 调整

观察杂乱线条的特征, 新建渐变映射图层, 调整到画面满意. 参考调整如下

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913121820.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210913121820.png?x-oss-process=image/format,jpg/interlace,1#center)

# 3 不足

就算是调整过后, 也依然存在一些未清理干净的线条需要手动进行清理, 且此方法在厚涂或者半厚涂的作品上表现并不好.

# 参考

1. [https://www.bilibili.com/video/BV1Uf4y1n7zK](https://www.bilibili.com/video/BV1Uf4y1n7zK)
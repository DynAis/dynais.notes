---
title: "Blender-MD动画数据流程"
# author: 
tags:
  - Blender
  - MD
date: '2022-04-17'
ShowToc: true
draft: false
---
从Blender导出动画人物到MD后导入回Blender的流程
<!--more-->

---

# 1 Blender → MD

使用 Alembic 的默认设置导出模型文件

MD中选择如下

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206211213795.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206211213795.png?x-oss-process=image/format,jpg/interlace,1#center)

注意帧率和单位匹配

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206211326777.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206211326777.png?x-oss-process=image/format,jpg/interlace,1#center])

# 2 MD → Blender

首先记得转一下衣服的四边面

选择导出, 这里有两个Alembic, 选择第二个

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206232203416.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220206232203416.png?x-oss-process=image/format,jpg/interlace,1#center)

# 3 MD → Blender 静帧

也可以选择FBX导出, 但是设置有点要求

![https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220208191019533.png](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/image-20220208191019533.png?x-oss-process=image/format,jpg/interlace,1#center)
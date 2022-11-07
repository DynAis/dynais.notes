---
title: PSpice模拟数据导入Excel工作流
tags:
  - PSpice
date: 2020-12-17
draft: true
---

基本思想是先保存到 csv 逗号分隔符文件再导入 Excel 里分析

<!--more-->

---

## 流程

在 PSpice 得到模拟数据后, 选中需要导出的曲线

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20201217162110.png#center)

看到它变红了

然后直接 `Ctrl + C` 就可以获得曲线数据

然后新建一个文本文档, 复制粘贴保存成 `.csv` 文件

直接导入 Excel 应该也是可行的, 但是由于改成了德国的计数方法, 这里的逗号和小数点会有问题, 先导入 csv 文件的话就没问题, 所以还是建议保存到 csv, 这样 Matlab 什么的也能用
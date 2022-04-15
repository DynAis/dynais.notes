---
title: 解决Python脚本在运行环境下依赖库缺失的问题
tags: 
  - Python
categories: 
  - 笔记 
  - Python
keywords: 
  - 库文件
  - python
thumbnailImagePosition: top
coverImage: 'https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725004705.jpg'
coverMeta: in
coverSize: partial
metaAlignment: center
abbrlink: ce920ebf
date: 2021-02-23 12:40:37
thumbnailImage:
---

在某一个虚拟环境中完成脚本后, 想要实际使用时可能会出现错误
{% image fancybox center clear group:default https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210223124433.png?x-oss-process=image/resize,h_2000/quality,q_90  %}
这是由于虚拟环境和运行环境不一致导致依赖库缺失无法`import`导致的

<!-- excerpt -->

## 问题描述
在某一个虚拟环境中完成脚本后, 想要实际使用时可能会出现错误
{% image fancybox center clear group:default https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210223124433.png?x-oss-process=image/resize,h_2000/quality,q_90  %}
这是由于虚拟环境和运行环境不一致导致依赖库缺失无法`import`导致的
<br>
<br>

## 解决方法
解决方式就是在编写脚本时, 对于第三方的库进行一次检测, 如果没有的话就进行`pip install`
```python
try:
    import regex as re
except ImportError:
    os.system('pip install regex')
    import regex as re
```
对于小脚本来说这样就足够了, 项目大的话不建议这样使用
---
title: "Spleeter实现背景人声轨道分离"
# author: 
date: '2022-04-17'
ShowToc: true
draft: false
---
使用spleeter的python包实现提取MP3文件的背景和人声轨道
<!--more-->

---


# 前置知识

- python

# 安装

```python
pip install spleeter
```

# DEMO - 分离人声和乐器

```python
spleeter separate -o 输出路径 源音频.mp3
```

# DEMO - 分离人声/贝斯/鼓/钢琴/其他

```python
spleeter separate -o 输出路径 -p spleeter:5stems 源音频.mp3
```

# 参考

- [https://github.com/deezer/spleeter](https://github.com/deezer/spleeter)
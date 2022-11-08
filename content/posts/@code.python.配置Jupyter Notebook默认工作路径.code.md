---
title: "配置Jupyter Notebook默认工作路径"
# author: 
tags:
  - Python
date: '2022-04-16'
ShowToc: true
draft: true
---

配置Jupyter Notebook默认工作路径
<!--more-->

---

## 方法

1. 在 Terminal 输入 `jupyter notebook --generate-config` 建立配置文件, 记录输出路径

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/202204162208323.png#center)


1. 在这个路径下找到 `jupyter_notebook_config.py` 文件, 修改文件

```python
## The directory to use for notebooks and kernels.
#c.NotebookApp.notebook_dir = ''
```

更改为

```python
## The directory to use for notebooks and kernels.
c.NotebookApp.notebook_dir = 'D:\your\dir'
```

注意改完之后如果使用快捷方式打开大概率会没用, 因为快捷方式里还带着一个 `-%USERFILE` 的后缀, 删掉就好了

# 参考

1. [https://blog.csdn.net/u014552678/article/details/62046638](https://blog.csdn.net/u014552678/article/details/62046638)
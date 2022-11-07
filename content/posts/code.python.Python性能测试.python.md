---
title: "Python性能测试"
# author: 
tags:
  - Python
  - cProfile
date: '2022-11-07'
ShowToc: true
draft: true
---
<!--more-->

---
## Usage
替换`YOUR_FUNKTION_NAME()`为自己的主函数. AND RUN!!!.
生成 `output._time.txt` 和 `output._calls.txt` 文件. 分别是对运行时函数按总花费时间的排序和总调用次数的排序.
```python
if __name__ == "__main__":

  # create peformence analysis

  import cProfile

  cProfile.run('YOUR_FUNKTION_NAME()', 'output.dat')

  

  import pstats

  from pstats import SortKey

  

  with open('output_time.txt',"w") as f:

    p = pstats.Stats('output.dat', stream=f)

    p.sort_stats("time").print_stats()

  

  with open('output_calls.txt',"w") as f:

    p = pstats.Stats('output.dat', stream=f)

    p.sort_stats("calls").print_stats()
```


---
title: "批处理"
# author: 
tags:
  - Batch
date: '2022-04-16'
ShowToc: true
draft: false
---

批处理基础语法参考
<!--more-->

---

## 基础命令

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/202204162209786.png#center)


**set**

- `/p` p for prompt 接收用户输入
- `/a` a for arithmetic 计算数学公式

**& && | ||**

- `&` 顺序执行多条命令，而不管命令是否执行成功
- `&&` 顺序执行多条命令，当碰到执行出错的命令后将不执行后面的命令
- `||` 顺序执行多条命令，当碰到执行正确的命令后将不执行后面的命令（即：只有前面命令执行错误时才执行后面命令）
- `|`管道命令 前一个命令的执行结果输出到后一个命令 `@(echo %%i | findstr "old ___")`
- `>` 清除文件中原有的内容后再写入
- `>>` 追加内容到文件末尾，而不会清除原有的内容主要将本来显示在屏幕上的内容输出到指定文件中指定文件如果不存在，则自动生成该文件

**if**

- 可以用 `exist` 判断目录下的文件 `if exist e:\b.txt (echo e盘下有b.txt) else (echo e盘下没有b.txt)`
- == - 等于
- EQU - 等于
- NEQ - 不等于
- LSS - 小于
- LEQ - 小于或等于
- GTR - 大于
- GEQ - 大于或等于

**for**

- 语法`for {%% | %}<variable> in (<set>) do <command> [<commandlineoptions>]`
- `/f` 解析文本, 很常用.
    - `delims` 做分隔符使用，只会保留分隔符之前的内容。若要填入多个分隔符，则写在等号后就好，中间无需加空格
    - `tokens` 选定分割之后的内容
- `/l` 使用一个迭代变量来设置`for /l %%i in (<start#>,<step#>,<end#>) do <command>`
- set 可以为很多东西,文件,dir的列表等等, 这样进行每行的迭代, 使用函数要包裹在`('')`中
- 下面列了一些可以对文件修饰的修饰符, 这些修饰符都可以组合, 如`%%~dpi`显示磁盘+路径

```
%%~I         - expands %I removing any surrounding quotes ("")
%%~fI        - 将%I扩展为一个完全合格的路径名称
%%~dI        - expands %I to a drive letter only
%%~pI        - 仅将%I扩展为一个路径
%%~nI        - 仅将%I扩展为一个文件名
%%~xI        - expands %I to a file extension only
%%~sI        - expanded path contains short names only
%%~aI        - expands %I to file attributes of file
%%~tI        - 将%I扩展为文件的日期/时间
%%~zI        - expands %I to size of file
%%~$PATH:I   - searches the directories listed in the PATH
               environment variable and expands %I to the
               fully qualified name of the first one found.
               If the environment variable name is not
               defined or the file is not found by the
               search, then this modifier expands to the
               empty string
```

**set**

- `/p` 用户输入赋值
- `/a` 数学计算赋值

**findstr**

- `/b` 如果位于行的开头则匹配模式。
- `/e` 如果位于行的末尾则匹配模式。
- `/l` 逐字地搜索字符串。
- `/r` 使用搜索串作为正则表达式。Findstr 将所有元字符解释为正则表达式，除非使用了 /l。
- `/s` 在当前目录和所有子目录中搜索匹配的文件。
- `/i` 指定搜索不区分大小写。

**dir**

- `/b` 只显示文件名
- `/s` 列出指定目录和所有子目录中出现的每个指定文件名。
- `/a:-d` 只显示那些具有你指定属性的目录和文件的名称

**del**

- `/q` 指定安静模式。不会提示你确认删除。
- `/s` 从当前目录和所有子目录中删除指定的文件。显示正在删除的文件的名称。

**mkdir**

**rd**

**type**

**call**

**copy**

**move**

**%CD%** 显示当前磁盘名

---

**列出目录下文件并查找字符**

```
:LOOP
for/f %%i in('dir/b/a-d') do @(echo %%i | findstr "old ___" && move %%i .\old && set /a count+=1)
if %count% leq 9 goto LOOP
```

## 参考

1. [https://www.w3cschool.cn/dosmlxxsc1/wvqyr9.html](https://www.w3cschool.cn/dosmlxxsc1/wvqyr9.html)
2. [https://www.jianshu.com/p/976b0dd64710](https://www.jianshu.com/p/976b0dd64710)
3. [https://blog.csdn.net/Joker_N/article/details/89838719](https://blog.csdn.net/Joker_N/article/details/89838719)
---
title: "UTF8编解码"
# author: 
tags:
  - UML
date: '2022-04-16'
ShowToc: true
draft: false
---

UTF8的基本知识

<!--more-->

---

## 1 Unicode

Unicode，联盟官方中文名称为统一码. 这是一个字符编码的标准, 就是给字符表里的抽象字符编上一个数字，也就是字符集合到一个整数集合的映射。这种映射称为编码字符集（CCS:Coded Character Set）,unicode 是属于这一层的概念，跟计算机里的什么进制啊没有任何关系，它是完全数学的抽象的. 

Unicode 称这个编号为这个字符的**码点,** 通常使用 `U+XXXX` 表示, U+后面的是十六进制字符.

比如

```
I 0049
t 0074
' 0027
s 0073
  0020
知 77e5
乎 4e4e
日 65e5
报 62a5
```

而如何有效的把这个编码映射到1和0的排列上, 就是UTF-8规定的事情.

## 2 UTF-8编码

以最朴素的想法来说, 直接将 Unicode 对应的字符编号转换为二进制会如何呢? 会造成不必要的空间浪费, 因为就编码理论来说, 出现概率小的字符拥有较小的编码长度是理所应当的. 

所以 UTF-8 出现了

UTF-8 是目前互联网上使用最广泛的一种 Unicode 编码方式，它的最大特点就是**可变长。它可以使用 1 - 4 个字节表示一个字符，根据字符的不同变换长度.**编码规则如下：

1. **对于单个字节的字符，第一位设为 0，后面的 7 位对应这个字符的 Unicode 码点**。因此，对于英文中的 0 - 127 号字符，**与 ASCII 码完全相同**。这意味着 ASCII 码那个年代的文档用 UTF-8 编码打开完全没有问题。
2. **对于需要使用 N 个字节来表示的字符（N > 1），第一个字节的前 N 位都设为 1，第 N + 1 位设为 0，剩余的 N - 1 个字节的前两位都设位 10，剩下的二进制位则使用这个字符的 Unicode 码点来填充(前0补足).**

编码规则如下：

[UTF-8编码](https://www.notion.so/83b1fb5d5d804a28bdc7dfc75f2eecf2)

根据上面编码规则对照表，进行 UTF-8 编码和解码就简单多了。下面以汉字“汉”为利，具体说明如何进行 UTF-8 编码和解码。

“汉”的 Unicode 码点是 0x6c49（110 1100 0100 1001），通过上面的对照表可以发现，0x0000 6c49 位于第三行的范围，那么得出其格式为 1110xxxx 10xxxxxx 10xxxxxx。接着，从“汉”的二进制数最后一位开始，从后向前依次填充对应格式中的 x，多出的 x 用 0 补上。这样，就得到了“汉”的 UTF-8 编码为 11100110 10110001 10001001，转换成十六进制就是 0xE6 0xB7 0x89。

解码的过程也十分简单：如果一个字节的第一位是 0 ，则说明这个字节对应一个字符；如果一个字节的第一位 1，那么连续有多少个 1，就表示该字符占用多少个字节。


## 参考

1. [https://www.zhihu.com/question/23374078](https://www.zhihu.com/question/23374078)
2. [https://zh.wikipedia.org/wiki/Unicode](https://zh.wikipedia.org/wiki/Unicode)
3. [https://liyucang-git.github.io/2019/06/17/彻底弄懂Unicode编码/](https://liyucang-git.github.io/2019/06/17/%E5%BD%BB%E5%BA%95%E5%BC%84%E6%87%82Unicode%E7%BC%96%E7%A0%81/)
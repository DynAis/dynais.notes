---
title: Latex公式查找表
tags:
  - LaTex
date: 2020-03-5
---
 在Markdown中插入数学公式的语法是 `$数学公式$` 和 `$$数学公式$$`.

## 行内公式

行内公式是可以让公式在文中与文字或其他东西混编，不独占一行.在数学模式下,符号会使用单独的字体,字母通常是倾斜的意大利体,数字和符号则是直立体.而且,数学符号之间的距离也与一般的水平模式不同:

| 示例         | 显示                                                         |
| ------------ | ------------------------------------------------------------ |
| `$2x+3y=34$` | ![2x+3y=34](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725005742.svg) |
| `2x+3y=34`   | 2x+3y=34                                                     |

因此,在排版数学公式时,即使没有特殊符号的算式如1+1=2,或者简单的一个字母变量![x](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725010108.svg),也要进入数学模式,使用`$1+1=2$`,`$x$`,而不是使用排版普通文字的方式

## 独立公式

独立公式单独占一行,不和其他文字混编

## 多行公式

在独立公式中使用\\来换行
 示例:

<!-- more -->

```ruby
$$   
2x+3y=34\\   
x+4y=25  
$$
```

显示:
 ![2x+3y=34\\ x+4y=25](https://math.jianshu.com/math?formula=2x%2B3y%3D34\\ x%2B4y%3D25)

## 常用符号

| 符号   | 示例                                                | 显示                                                         |
| ------ | --------------------------------------------------- | ------------------------------------------------------------ |
| 上下标 | `S=a_{1}^2+a_{2}^2+a_{3}^2$`                        | ![S=a_{1}^2+a_{2}^2+a_{3}^2](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725005759.svg) |
| 括号   | `$f(x, y) = 100 * \lbrace[(x + y) * 3] - 5\rbrace$` | ![f(x, y) = 100 * \lbrace[(x + y) * 3] - 5\rbrace](https://math.jianshu.com/math?formula=f(x%2C%20y)%20%3D%20100%20*%20%5Clbrace%5B(x%20%2B%20y)%20*%203%5D%20-%205%5Crbrace) |
| 分数   | `$\frac{1}{3} 与 \cfrac{1}{3}$`                     | ![\frac{1}{3} 与 \cfrac{1}{3}](https://math.jianshu.com/math?formula=%5Cfrac%7B1%7D%7B3%7D%20%E4%B8%8E%20%5Ccfrac%7B1%7D%7B3%7D) |
| 开方   | `$\sqrt[3]{X}$`和`$\sqrt{5 - x}$`                   | ![\sqrt[3]{X}](D:\WorkSpace\.Typora Images Hub\math-1583415699231.svg)和![\sqrt{5 - x}](https://math.jianshu.com/math?formula=%5Csqrt%7B5%20-%20x%7D) |

## 其他字符

### 关系运算符

| 代码       | 符号                                                         |
| ---------- | ------------------------------------------------------------ |
| \pm        | ![\pm](https://math.jianshu.com/math?formula=%5Cpm)          |
| \times     | ![\times](https://math.jianshu.com/math?formula=%5Ctimes)    |
| \div       | ![\div](https://math.jianshu.com/math?formula=%5Cdiv)        |
| \mid       | ![\mid](https://math.jianshu.com/math?formula=%5Cmid)        |
| \nmid      | ![\nmid](https://math.jianshu.com/math?formula=%5Cnmid)      |
| \cdot      | ![\cdot](https://math.jianshu.com/math?formula=%5Ccdot)      |
| \circ      | ![\circ](https://math.jianshu.com/math?formula=%5Ccirc)      |
| \ast       | ![\ast](https://math.jianshu.com/math?formula=%5Cast)        |
| \bigodot   | ![\bigodot](https://math.jianshu.com/math?formula=%5Cbigodot) |
| \bigotimes | ![\bigotimes](https://math.jianshu.com/math?formula=%5Cbigotimes) |
| \bigoplus  | ![\bigoplus](https://math.jianshu.com/math?formula=%5Cbigoplus) |
| \leq       | ![\leq](https://math.jianshu.com/math?formula=%5Cleq)        |
| \geq       | ![\geq](https://math.jianshu.com/math?formula=%5Cgeq)        |
| \neq       | ![\neq](https://math.jianshu.com/math?formula=%5Cneq)        |
| \approx    | ![\approx](https://math.jianshu.com/math?formula=%5Capprox)  |
| \equiv     | ![\equiv](https://math.jianshu.com/math?formula=%5Cequiv)    |
| \sum       | ![\sum](https://math.jianshu.com/math?formula=%5Csum)        |
| \prod      | ![\prod](https://math.jianshu.com/math?formula=%5Cprod)      |

### 对数运算符

| 代码 | 符号                                                  |
| ---- | ----------------------------------------------------- |
| \log | ![\log](https://math.jianshu.com/math?formula=%5Clog) |
| \lg  | ![\lg](https://math.jianshu.com/math?formula=%5Clg)   |
| \ln  | ![\ln](https://math.jianshu.com/math?formula=%5Cln)   |

### 三角运算符

| 代码   | 符号                                                      |
| ------ | --------------------------------------------------------- |
| \bot   | ![\bot](https://math.jianshu.com/math?formula=%5Cbot)     |
| \angle | ![\angle](https://math.jianshu.com/math?formula=%5Cangle) |
| \sin   | ![\sin](https://math.jianshu.com/math?formula=%5Csin)     |
| \cos   | ![\cos](https://math.jianshu.com/math?formula=%5Ccos)     |
| \tan   | ![\tan](https://math.jianshu.com/math?formula=%5Ctan)     |
| \cot   | ![\cot](https://math.jianshu.com/math?formula=%5Ccot)     |
| \sec   | ![\sec](https://math.jianshu.com/math?formula=%5Csec)     |
| \csc   | ![\csc](https://math.jianshu.com/math?formula=%5Ccsc)     |

### 微积分运算符

| 代码       | 符号                                                         |
| ---------- | ------------------------------------------------------------ |
| \prime     | ![\prime](https://math.jianshu.com/math?formula=%5Cprime)    |
| \int       | ![\int](https://math.jianshu.com/math?formula=%5Cint)        |
| \iint      | ![\iint](https://math.jianshu.com/math?formula=%5Ciint)      |
| \iiint     | ![\iiint](https://math.jianshu.com/math?formula=%5Ciiint)    |
| \oint      | ![\oint](https://math.jianshu.com/math?formula=%5Coint)      |
| \lim       | ![\lim](https://math.jianshu.com/math?formula=%5Clim)        |
| \infty     | ![\infty](https://math.jianshu.com/math?formula=%5Cinfty)    |
| \nabla     | ![\nabla](https://math.jianshu.com/math?formula=%5Cnabla)    |
| \mathrm{d} | ![\mathrm{d}](https://math.jianshu.com/math?formula=%5Cmathrm%7Bd%7D) |

### 集合运算符

| 代码      | 符号                                                         |
| --------- | ------------------------------------------------------------ |
| \emptyset | ![\emptyset](https://math.jianshu.com/math?formula=%5Cemptyset) |
| \in       | ![\in](https://math.jianshu.com/math?formula=%5Cin)          |
| \notin    | ![\notin](https://math.jianshu.com/math?formula=%5Cnotin)    |
| \subset   | ![\subset](https://math.jianshu.com/math?formula=%5Csubset)  |
| \subseteq | ![\subseteq](https://math.jianshu.com/math?formula=%5Csubseteq) |
| \supseteq | ![\supseteq](https://math.jianshu.com/math?formula=%5Csupseteq) |
| \bigcap   | ![\bigcap](https://math.jianshu.com/math?formula=%5Cbigcap)  |
| \bigcup   | ![\bigcup](https://math.jianshu.com/math?formula=%5Cbigcup)  |
| \bigvee   | ![\bigvee](https://math.jianshu.com/math?formula=%5Cbigvee)  |
| \bigwedge | ![\bigwedge](https://math.jianshu.com/math?formula=%5Cbigwedge) |
| \biguplus | ![\biguplus](https://math.jianshu.com/math?formula=%5Cbiguplus) |
| \bigsqcup | ![\bigsqcup](https://math.jianshu.com/math?formula=%5Cbigsqcup) |

### 希腊字母

| 代码     | 大写                                                         | 代码     | 小写                                                         |
| -------- | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| A        | ![A](https://math.jianshu.com/math?formula=A)                | \alpha   | ![\alpha](https://math.jianshu.com/math?formula=%5Calpha)    |
| B        | ![B](https://math.jianshu.com/math?formula=B)                | \beta    | ![\beta](https://math.jianshu.com/math?formula=%5Cbeta)      |
| \Gamma   | ![\Gamma](https://math.jianshu.com/math?formula=%5CGamma)    | \gamma   | ![\gamma](https://math.jianshu.com/math?formula=%5Cgamma)    |
| \Delta   | ![\Delta](https://math.jianshu.com/math?formula=%5CDelta)    | \delta   | ![\delta](https://math.jianshu.com/math?formula=%5Cdelta)    |
| E        | ![E](https://math.jianshu.com/math?formula=E)                | \epsilon | ![\epsilon](https://math.jianshu.com/math?formula=%5Cepsilon) |
| Z        | ![Z](https://math.jianshu.com/math?formula=Z)                | \zeta    | ![\zeta](https://math.jianshu.com/math?formula=%5Czeta)      |
| H        | ![H](https://math.jianshu.com/math?formula=H)                | \eta     | ![\eta](https://math.jianshu.com/math?formula=%5Ceta)        |
| \Theta   | ![\Theta](https://math.jianshu.com/math?formula=%5CTheta)    | \theta   | ![\theta](https://math.jianshu.com/math?formula=%5Ctheta)    |
| I        | ![I](https://math.jianshu.com/math?formula=I)                | \iota    | ![\iota](https://math.jianshu.com/math?formula=%5Ciota)      |
| K        | ![K](https://math.jianshu.com/math?formula=K)                | \kappa   | ![\kappa](https://math.jianshu.com/math?formula=%5Ckappa)    |
| \Lambda  | ![\Lambda](https://math.jianshu.com/math?formula=%5CLambda)  | \lambda  | ![\lambda](https://math.jianshu.com/math?formula=%5Clambda)  |
| M        | ![M](https://math.jianshu.com/math?formula=M)                | \mu      | ![\mu](https://math.jianshu.com/math?formula=%5Cmu)          |
| N        | ![N](https://math.jianshu.com/math?formula=N)                | \nu      | ![\nu](https://math.jianshu.com/math?formula=%5Cnu)          |
| Xi       | ![Xi](https://math.jianshu.com/math?formula=Xi)              | \xi      | ![\xi](https://math.jianshu.com/math?formula=%5Cxi)          |
| O        | ![O](https://math.jianshu.com/math?formula=O)                | \omicron | ![\omicron](https://math.jianshu.com/math?formula=%5Comicron) |
| \Pi      | ![\Pi](https://math.jianshu.com/math?formula=%5CPi)          | \pi      | ![\pi](https://math.jianshu.com/math?formula=%5Cpi)          |
| P        | ![P](https://math.jianshu.com/math?formula=P)                | \rho     | ![\rho](https://math.jianshu.com/math?formula=%5Crho)        |
| \Sigma   | ![\Sigma](https://math.jianshu.com/math?formula=%5CSigma)    | \sigma   | ![\sigma](https://math.jianshu.com/math?formula=%5Csigma)    |
| T        | ![T](https://math.jianshu.com/math?formula=T)                | \tau     | ![\tau](https://math.jianshu.com/math?formula=%5Ctau)        |
| \Upsilon | ![\Upsilon](https://math.jianshu.com/math?formula=%5CUpsilon) | \upsilon | ![\upsilon](https://math.jianshu.com/math?formula=%5Cupsilon) |
| \Phi     | ![\Phi](https://math.jianshu.com/math?formula=%5CPhi)        | \phi     | ![\phi](https://math.jianshu.com/math?formula=%5Cphi)        |
| X        | ![X](https://math.jianshu.com/math?formula=X)                | \chi     | ![\chi](https://math.jianshu.com/math?formula=%5Cchi)        |
| \Psi     | ![\Psi](https://math.jianshu.com/math?formula=%5CPsi)        | \psi     | ![\psi](https://math.jianshu.com/math?formula=%5Cpsi)        |
| \Omega   | ![\Omega](https://math.jianshu.com/math?formula=%5COmega)    | \omega   | ![\omega](https://math.jianshu.com/math?formula=%5Comega)    |

- 需要大写希腊字母，将命令首字母大写即可。
  \Gamma呈现为

  ![img](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210317223633.webp)

- 若需要斜体希腊字母，将命令前加上var前缀即可。

  ![img](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20210317223637.png)

## 向量和复数

普通的变量x:`x`:$x$

粗体1：使用`\boldsymbol{}`进行加粗，如：`\boldsymbol{x}`:$\boldsymbol{x}$

粗体2：使用`\mathbf{}`进行加粗，如：`\mathbf{x}`:$\mathbf{x}$

带箭头的向量：使用`\vec{}`使向量带箭头，如`\vec{x}`:$\vec{x}$

复数表示: `\underline{}` 表示为 $\underline{U}$ 

## 绝对值

使用`\vert`:$\vert U \vert$

## 字体

![img](https:////upload-images.jianshu.io/upload_images/436556-45c8673c41af7c42.png?imageMogr2/auto-orient/strip|imageView2/2/w/446/format/webp)

## 分组

![img](https:////upload-images.jianshu.io/upload_images/436556-434dd3242e693d70.png?imageMogr2/auto-orient/strip|imageView2/2/w/375/format/webp)

## 括号

![img](https:////upload-images.jianshu.io/upload_images/436556-6ef5dd4fd56680f9.png?imageMogr2/auto-orient/strip|imageView2/2/w/599/format/webp)

##  求和、极限与积分

![img](https:////upload-images.jianshu.io/upload_images/436556-fb2604765d03c8d8.png?imageMogr2/auto-orient/strip|imageView2/2/w/526/format/webp)

### 空格

![img](https:////upload-images.jianshu.io/upload_images/436556-f9b9a026db748466.png?imageMogr2/auto-orient/strip|imageView2/2/w/264/format/webp)

## 矩阵

### 基本语法

起始标记`\begin{matrix}`，结束标记`\end{matrix}`
每一行末尾标记`\\\`，行间元素之间以`&`分隔
举例:

```ruby
$$\begin{matrix}
1&0&0\\
0&1&0\\
0&0&1\\
\end{matrix}$$
```

呈现为：



![img](https:////upload-images.jianshu.io/upload_images/436556-1548fa2d1079ef70.png?imageMogr2/auto-orient/strip|imageView2/2/w/113/format/webp)

### 矩阵边框

- 在起始、结束标记处用下列词替换 `matrix`
- `pmatrix` ：小括号边框
- `bmatrix` ：中括号边框
- `Bmatrix` ：大括号边框
- `vmatrix` ：单竖线边框
- `Vmatrix` ：双竖线边框

### 省略元素

- 横省略号：`\cdots`
- 竖省略号：`\vdots`
- 斜省略号：`\ddots`

```ruby
$$\begin{bmatrix}
{a_{11}}&{a_{12}}&{\cdots}&{a_{1n}}\\
{a_{21}}&{a_{22}}&{\cdots}&{a_{2n}}\\
{\vdots}&{\vdots}&{\ddots}&{\vdots}\\
{a_{m1}}&{a_{m2}}&{\cdots}&{a_{mn}}\\
\end{bmatrix}$$
```

呈现为：



![img](https:////upload-images.jianshu.io/upload_images/436556-72c03690ce9e63b8.png?imageMogr2/auto-orient/strip|imageView2/2/w/235/format/webp)

### 阵列

![img](https:////upload-images.jianshu.io/upload_images/436556-19f8205a2b599b86.png?imageMogr2/auto-orient/strip|imageView2/2/w/384/format/webp)

举例

```swift
$$\begin{array}{c|lll}
{↓}&{a}&{b}&{c}\\
\hline
{R_1}&{c}&{b}&{a}\\
{R_2}&{b}&{c}&{c}\\
\end{array}$$
```

呈现为

![img](https:////upload-images.jianshu.io/upload_images/436556-84dac3a98e0e44a9.png?imageMogr2/auto-orient/strip|imageView2/2/w/154/format/webp)

### 方程组

- 需要cases环境：起始、结束处以{cases}声明

举例

```cpp
$$\begin{cases}
a_1x+b_1y+c_1z=d_1\\
a_2x+b_2y+c_2z=d_2\\
a_3x+b_3y+c_3z=d_3\\
\end{cases}
$$
```

呈现为

![img](https:////upload-images.jianshu.io/upload_images/436556-8e608fa9d8906bf1.png?imageMogr2/auto-orient/strip|imageView2/2/w/250/format/webp)


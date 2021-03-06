---
title: '[DA] DuinoAccess'
tags:
  - DuinoAccess
date: '2020-08-20'
---

这次也是因为闲的在家没有事情做，所以又给自己开了一个新坑，其实蛮早以前就有过想做一个电脑上能用的指纹锁的想法了，但是一直没有动手，刚好这次有机会，并且也是刚刚新组了一台电脑，就想着要把这个项目给做了。

这个项目的一个主要的灵感来源是@[稚晖君](https://space.bilibili.com/20259914/dynamic)很早以前发在Arduino论坛上的一个项目 ([Link: 如何制作一个带指纹识别的机械键盘](https://www.arduino.cn/thread-86889-1-3.html)), 这次项目的的主要思路都和他的差不多，只不过我想做成独立的一个模块，并且最好能够实现便携功能，也就是说如果可以的话我想加上蓝牙的功能

然后这次的文章大概也会写好几部分，具体取决于我最后能不能最后好好完成这个项目...

这是一个开源项目，后续也会一直更新进度，对你有帮助的话可以给我个星星，传送门：https://github.com/DynAis/duino-access

<!--more-->

---

## 0x01 - 核心部分元器件选型

这次的目标是能够使用指纹解锁的方式让电脑自动解锁，思路是使用指纹模块给出信号+单片机模拟键盘输入的简单思路，由于整体的体积要求越小越好，所以元件的选型基本没有选择



| 使用模块                                                     | 价格      |
| ------------------------------------------------------------ | --------- |
| arduino-pro-micro (VCC 5v or 3.3v)                           | 19.80 CNY |
| HN0610 指纹模块                                              | 45.00 CNY |
| AMS1117-3.3v/5v 降压模块 (假如使用5v的arduino，3.3v的不需要) | 1.29 CNY  |
| 蜂鸣器、导线若干                                             | -         |



之所以没有用稚晖的那个FPM3X指纹模块的原因是因为那个好像在TB上已经快找不到了，只剩下最后一家而且卖的很贵，所以当时就选择了这个卖得最好的来做(有几天自闭的时候非常后悔这个选择)，并且从外观上来说我更喜欢这款一点


---

## 0x02 - 环境选择与搭建

### VSCode + PlatformIO

整个环境方面没有使用传统的 ArduinoIDE 来做，而是选择的使用 VSCode 来完成这次的项目，主要原因是为了以后做其他单片机项目的时候也都统一到 VSCode上去，这样整个一致性会比较好

最后选择了 VSCode 的 PlatformIO 拓展

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184349.png?x-oss-process=image/format,jpg/interlace,1#center)

直接在 VSCode 的拓展商店里搜索即可，点击安装即可安装插件，不用动什么脑子，安装过程会有些慢需要耐心等待一会，安装完成后如果成功了你应该可以在左下角看到这个小图标

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184359.png?x-oss-process=image/format,jpg/interlace,1#center)

恭喜，如果你看到了这个小房子，那你基本就是安装成功了，但是由于各种各样的原因，你也很有可能等了半天他也还是在转圈圈加载，像我一样

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184405.png?x-oss-process=image/format,jpg/interlace,1#center)

那么大概率他是不能自己装上了，我们只能来手动安装

首先，如果你安装失败了，请先卸载原来的安装失败的 PlatformIO ，重启 VSCode，之后在VSCode的终端里输入

`sudo pip --no-cache-dir install -U platformio`

等待他安装完成，重启VSCode，重新去商店点一下安装，就可以顺利的装上了

如果依旧不行，可以尝试: 移除Anaconda(假如你安装了Anaconda环境)、安装Python2.7版本并且添加进环境变量、安装Python最新版本并添加进环境变量，如果这也不行，那就尝试使用ArduinoIDE吧(不过这样也许需要稍微改动下代码)

### PlatformIO开发准备

点击Home按钮打开 PlatformIO 主界面，new project 后选择对应的板子，他会进行自动的初始化

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184414.png?x-oss-process=image/format,jpg/interlace,1#center)

初始化完成后，在src文件夹里就是我们的main文件

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184421.png?x-oss-process=image/format,jpg/interlace,1#center)

PlatformIO 和 ArduinoIDE 不同的地方就是，他是使用cpp文件来进行编译上传的，而不是ino文件，所以每个需要用到 Arduino 库的文件中，都需要包含`#include "Arduino.h"`才能够使用

此外，比较麻烦的一点是，对于某些库的支持，也是需要我们手动来加入的，比如这块 Pro Micro 支持的HID键盘和鼠标的功能，就需要我们手动加入

首先打开刚才的Home界面，在左边一栏里可以找到 Libraries

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184426.png?x-oss-process=image/format,jpg/interlace,1#center)

搜索`keyboard`，找到这个 Arduino 的官方库文件安装

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184431.png?x-oss-process=image/format,jpg/interlace,1#center)

安装完成以后，到左边的资源管理器，找到`platformio.ini`这个文件![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184436.png?x-oss-process=image/format,jpg/interlace,1#center)

在文件最后加入

```ini
lib_deps = 
    Keyboard
```

告诉他我们要调用这个库，这样就完成了，可以开始硬件部分的测试了

---

## 0x03 - 硬件部分

**一定要注意指纹模块的供电是3.3v，使用5v虽然不会烧坏模块但是会无法工作(当初因为这个原因卡了好久不知道哪错了)**

指纹模块的话是线给剪了直接焊在了板子上，有点粗糙

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184449.jpg?x-oss-process=image/format,jpg/interlace,1#center)

看不清楚的话也可以看源文件里 `/lib/HN0610/pinDef.h` 里的内容

最后附上Micro的引脚图

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184454.png?x-oss-process=image/format,jpg/interlace,1#center)


### 测试指纹模块

修改 `/src/min.cpp` 文件中参数调整宏定义区域的参数  `DASTATE` 就可以设定当前运行在什么模式下，由于是测试，就把值改为0，运行在检测手指模式上，其他模式的定义也在下面给出

| 功能实现                                     | DASTATE值 |
| -------------------------------------------- | --------- |
| 检测手指按压                                 | 0         |
| 指纹注册                                     | 1         |
| 验证指纹(最后留这一个)                       | 2         |
| 检测手指按压后输出硬件信息(需要打开电脑串口) | 3         |
| 清除所有指纹信息                             | 4         |

 点击上传烧录进Arduino

如果没有问题的话，按下手指蜂鸣器就会鸣响了

---

## 0x04 - 遇到的坑和问题

### 1. 底层数据类型定义问题

通常来说，开发单片机会定义一系列的UINT

在这次，定义文件写在了 `hzTypes.h` 文件里，其中对于UINT32的定义出现了兼容错误

原始内容是

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184458.png?x-oss-process=image/format,jpg/interlace,1#center)

我猜测可能是由于他们使用的单片机上int是32位，所以能够正常运行，而在Arduino上，int并不是32位的，long才是，所以需要改为

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184502.png?x-oss-process=image/format,jpg/interlace,1#center)


### 2.电源的坑

已经说过了，不过这次也是因为在家里没有万用表的缘故，并且提醒，虽然原理图上有一个SJ1来控制Micro的输出电压是5v还是3.3v，但是你并不可以通过连接或者断开这个引脚来达到修改电压的目的，因为5v的Micro和3.3v的Micro主频也是不一样的，这会导致工作不稳定

并且很有可能改了也没有作用(对于很多国产板)

![](https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200820184513.png?x-oss-process=image/format,jpg/interlace,1#center)

### 3.注意Micro的中断脚

因为这个指纹识别模块还有自动休眠的功能，所以虽然我现在并没有使用，但是很有可能会用到这个模块的中断信号，那么就要注意Micro的中断引脚定义和Uno是不一样的

| PIN  | 中断号 |
| ---- | ------ |
| 3    | 0      |
| 2    | 1      |
| 0    | 2      |
| 1    | 3      |
| 7    | 6      |

---

## 0x05 - 后续开发

### 库HN610

| 文件名   | 内容                     |
| -------- | ------------------------ |
| auth     | 通讯签名算法(默认不签名) |
| fp       | 大部分能直接用的API      |
| fpmComm  | 模块命令API              |
| hzDevice | 串口通信底层             |
| pinDef   | 主板引脚定义             |
| hzTypes  | 数据类型定义             |


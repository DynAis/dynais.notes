---
title: PSpice中常用的Cursor查询命令
tags:
  - PSpice
categories:
  - 笔记
  - PSpice
keywords:
  - cursor
  - pspice
thumbnailImage: 'https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20201217161006.png'
thumbnailImagePosition: top
coverImage: 'https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725004705.jpg'
coverMeta: in
coverSize: partial
metaAlignment: center
abbrlink: 457ee858
date: 2020-12-17 00:00:00
---

受够了在 Probe 窗口中用鼠标拖 Cursor 来找结果数据了, 所以想找一下 Probe 的 SerchCommand 结果连官方用户指导里都找不到, 好不容易才在帮助文档里找到了, 写文档的真不是人, 记录一下防止以后忘了

Orcad Pspice版本: 9.1 Student

<!-- excerpt -->

## 概述

---

受够了在 Probe 窗口中用鼠标拖 Cursor 来找结果数据了, 所以想找一下 Probe 的 SerchCommand 结果连官方用户指导里都找不到, 好不容易才在帮助文档里找到了, 写文档的真不是人, 记录一下防止以后忘了

Orcad Pspice版本: 9.1 Student

文档进入方法:

{% image fancybox center clear group:default https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20201217161535.png 100% 100% " " %}

Win10还要上网找一下**win32hlp.exe**装一下才能看, 下载: [**win32hlp.exe**](http://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/storage/win10%E7%9A%84winhlp32%E8%A7%A3%E6%B1%BA%E6%96%B9%E6%A1%88.zip)

路径:

{% image fancybox center clear group:default https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20201217161557.png 50% 50% " " %}

<br/>

## 语法

---

`search	[direction]	[/start_point/]	[#consecutive_points#]	[(range_x [,range_y])]	[for]	[repeat:]	<condition>`

能把搜索语法写这么麻烦我真的服

<br/>

## 常用范例

---

其实语法不需要打全称, 是接收缩写的, 但是文档里一点没说

常用的是:

| example              | describtion                                   |
| -------------------- | --------------------------------------------- |
| `sf xv (这里是数字)` | 向前找到下一个X坐标最符合当前用户输入数字的点 |
| `sf le (这里是数字)` | 向前找到下一个Y坐标最符合当前用户输入数字的点 |

`sf` 是 **SerchForword** 的缩写, `xv` 是 **XValue** 的缩写, `le` 是 **LEvel** 的缩写

更加具体的可以在语法里的 `<condition>` 下找到
---
title: OpenCV中人脸识别的Haar实现
date: 2020-02-6
tags:
  - OpenCV
  - 数字图像处理
categories:
  - 项目
  - harr-face-detect
thumbnailImage: 
thumbnailImagePosition: 
coverImage: https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725004705.jpg
coverMeta: in
coverSize: partial
metaAlignment: center
abbrlink: dd5a240f
---

本次项目的计划是在短时间内制作出可以高准确度检测人脸并返回面部相对坐标的程序, 在经过参考他人的程序与查阅资料后采用了OpenCV内建的Haar级联器进行人脸的检测. 因为综合考虑可知Haar检测有准确率高, 速度快, 原理简单的优点, 虽然对于人脸侧面的检测不理想, 但是对于本次项目来说已经足够, 并且OpenCV已经有内建的Haar级联器, 以及训练好的数据集, 非常易于使用, 大大降低了项目的难度.

<!-- excerpt -->

## 项目总结_人脸识别的Haar实现

##### 项目历时:	2020.2.3 - 2020.2.5

##### 负责人:	Dynais

##### 项目花费:	无

##### 报告撰写时间: 2020.2.6

----------------------



### 项目概述

本次项目的计划是在短时间内制作出可以高准确度检测人脸并返回面部相对坐标的程序, 在经过参考他人的程序与查阅资料后采用了OpenCV内建的Haar级联器进行人脸的检测. 因为综合考虑可知Haar检测有准确率高, 速度快, 原理简单的优点, 虽然对于人脸侧面的检测不理想, 但是对于本次项目来说已经足够, 并且OpenCV已经有内建的Haar级联器, 以及训练好的数据集, 非常易于使用, 大大降低了项目的难度.



### 目录

- **第一部分**	部分原理粗解

  - 1.1	图像压缩
  - 1.2    直方图均衡化
  - 1.3    Haar特征检测

  

  

- **第二部分**    软件结构设计与实现



- **第三部分**    难点与优化方法

  - 3.1    难点一:	面部检测速度过慢

  

- **第四部分**    总结

  - 4.1    不足之处
  - 4.2    总结

  

- **第五部分**    参考文献





-------------------------



## 第一部分 部分原理粗解

### 1.1 图像压缩

对原图多个像素求和后取平均值, 得到一个新的像素值, 作为目标图像的像素值, 这样得到的新图像就是经过了压缩的原图像, 原理过于简单就不详细展开



### 1.2 直方图均衡化

[0]: https://www.jianshu.com/p/902126aa054e	"引用"

##### 直方图

建立一个桶, 将一幅图像的某一个通道的像素值进行桶排序并可视化, 呈现出来的图像称为直方图

一幅灰度图像的直方图通常如下:



[图没了]



直方图可以直观的反应图像上的像素值分布情况, 如:

![图1 4种基本的图像类型：暗图像、亮图像、低对比度图像、高对比度图像及其对应的直方图](https://img-blog.csdnimg.cn/20181123160536532.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NjaHdlaW5fdmFu,size_16,color_FFFFFF,t_70)



**直方图均衡化**

直方图均衡化是将原图像通过某种变换，得到一幅灰度直方图为均匀分布的新图像的方法.

直方图均衡化方法的基本思想是对在图像中像素个数多的灰度级进行展宽，而对像素个数少的灰度级进行缩减. 从而达到清晰图像的目的.

**将原图的像素值进行重新映射, 使直方图分布更加均匀, 达到了加强图像对比度的目的.**

具体解析见:

[直方图均衡化](https://blog.csdn.net/schwein_van/article/details/84336633)



### 1.3 Haar特征检测

Haar 特征检测部分, 由于已经有大量的博客详细描述过了, 所以不再浪费时间写

值得一提的是原作者的论文《Robust Real-Time Face Detection》是人脸检测的经典论文, 虽然读起来很困难(更何况是英文) 但还是值得一读, 如果希望深入了解的话

更多博客文章: 印象笔记关键字: **Haar**





----------------------



## 第二部分 软件结构设计与实现方法

文件夹"OpenCV_FaceDetectPro"中包含了两个.cpp文件:

- OpenCV_Process.cpp	包括人脸检测函数及其相关调用函数
- OpenCV_main.cpp    程序主入口



### 人脸检测流程

人脸检测(优化后的版本)的步骤分为:

- 识别标志位, 判断当前状态是检测还是跟踪

- 对摄像头当前采集图像进行分割
- 灰度化
- 压缩
- 直方图均衡化
- Haar特征检测
- 返回人脸位置



### 相关实现

##### 状态识别

由于时间复杂度问题(在下一章会说到), 采用了检测和跟踪分开的思路, 主要的思路是降低输入图像的大小. 采用每次检测完人脸后进行标志的判断为方法, 确定程序运行在那种状态下.

对于检测和跟踪模式, 使用了不同的思路来进行图像分割

##### Haar

直接使用了现成的数据, 自己并不会训练, 直接调用OpenCV的 CascadeClassifier 类实现



--------------------



## 第三部分 难点与优化方法

### 3.1 难点一: 面部检测速度过慢

未优化前的程序, 每次读入摄像头图像后直接进行灰度化与直方图均衡化, 然后进行全图的面部检测, 并且没有面部跟踪的实现, 导致每次图像的处理时间非常长, 达到了每帧图像0.8秒.

针对时间过长的问题, 首先引入了面部识别的标志位, 每次程序识别到面部时, 打开标志位, 然后在接下来的循环里只根据上次判断的面部位置截取小块图像进行判断,大大降低处理时间

其次, 使用图像压缩, 使待处理图像处于一个大小和准确度都可以接受的点上.

**引入后, 面部检测的时间从0.8秒降低到0.04秒**



**部分代码:**

**图像压缩**(前置函数为自己写的areaAvarage())

```
/****************************************************
*   Function:
*   用于图像压缩函数zipImg, 基于周边像素求出当前像素值
*
*   Note:
*   算法用左上像素求, 不知道会不会失真
*
*
******************************************************/

uchar areaAvarage(Mat src, Point pos, int channal, int gain) {
    int pixel = 0;

    if (src.channels() != 1) {
        int i, j;
        for (i = 0; i < gain; i++) {
            for (j = 0; j < gain; j++) {
                pixel += src.at<Vec3b>(pos.y - j, pos.x - i)[channal];
            }
        }
        pixel /= (gain * gain);
        return saturate_cast<uchar>(pixel);
    }
    else {
        int i, j;
        for (i = 0; i < gain; i++) {
            for (j = 0; j < gain; j++) {
                pixel += src.at<uchar>(pos.y - j, pos.x - i);
            }
        }
        pixel /= (gain * gain);
        return saturate_cast<uchar>(pixel);
    }
}



/****************************************************
*   Function:
*   图像压缩 gain^2 倍,长宽变为原先 1/gain
*
*   Note:
*	速度还是不够理想
*   留出了一圈白边
*
******************************************************/

void zipImg(Mat& src, Mat& dst, int gain) {
    dst = Mat(src.size() / gain, src.type());
    int i, j;

    if (src.channels() != 1) {
        //遍历
        for (i = 1; i < dst.cols - 1; i++) {
            for (j = 1; j < dst.rows - 1; j++) {
                uchar b, g, r;
                int realpos_x = i * gain;
                int realpos_y = j * gain;
                Point pos(realpos_x, realpos_y);

                //对周边像素求均值,赋值给新图
                b = areaAvarage(src, pos, 0, gain);
                g = areaAvarage(src, pos, 1, gain);
                r = areaAvarage(src, pos, 2, gain);
                dst.at<Vec3b>(j, i) = { b,g,r };
            }
        }
    }
    else {
        for (i = 1; i < dst.cols - 1; i++) {
            for (j = 1; j < dst.rows - 1; j++) {
                uchar g;
                int realpos_x = i * gain;
                int realpos_y = j * gain;
                Point pos(realpos_x, realpos_y);

                //对周边像素求均值,赋值给新图
                g = areaAvarage(src, pos, 1, gain);
                dst.at<uchar>(j, i) = g;
            }
        }
    }
}
```





--------------------------



## 第四部分 总结

### 4.1    不足之处

- 虽然采用检测与跟踪同样裁剪画面的方法, 但是效果其实并不理想, 速度提升微弱
- 面部检测对侧脸准确性几乎没有
- 光照优化有待加强
- 速度还是不够快
- 脸太大或太小检测不了

### 4.2    总结

总的来说这次项目还是挺成功的, 在几天以内就完成了, 虽然借由了大量API, 但原理也还是有所了解的. 接下来的任务是使他能够在树莓派上也能正常运行. 




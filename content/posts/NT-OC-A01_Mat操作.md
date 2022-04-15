---
title: OpenCV学习笔记01-Mat操作
tags:
  - OpenCV
  - 数字图像处理
categories:
  - 笔记
  - OpenCV
keywords:
- opencv
- mat
thumbnailImage: https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200724212717.png
thumbnailImagePosition:
coverImage: https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725004705.jpg
coverMeta: in
coverSize: partial
metaAlignment: center
abbrlink: f8bbd26a
date: 2020-01-14 00:00:00
---


### 完成

- 自己创建指定mat
- 用算法创建mat
- 克隆mat



### 相关函数

```c++
mat.clone();
mat.copyTo();

(1) Mat::Mat()
(2) Mat::Mat(int rows, int cols, int type)
(3) Mat::Mat(Size size, int type)
(4) Mat::Mat(int rows, int cols, int type, constScalar& s)
(5) Mat::Mat(Size size, int type, constScalar& s)
(6) Mat::Mat(const Mat& m)
    
mat.ptr<uchar>

```



### 实现

使用函数克隆一个一样的图

使用函数创建空白图(全0和全255)

使空白图成为渐变灰度图

使空白图成为渐变色度图

<!-- more -->

### 笔记

- **关于clone() \ copyTo() 和 直接赋值的区别**

  clone和copyTo是直接重新创建一个新的内存空间

  而直接赋值则是一个类似传递的作用,这样直接修改B的内容也会影响到A

  

- **区分Scalar和Vec3b**

  Scala指标量,Vec指向量

  Vec类似于C++中的Vector 也就是说可用{}赋值

  Scala我现在只知道在初始化中可用

  

### 相关

无



### 源

```c++
// OpenCV_Template.cpp : 此文件包含 "main" 函数。程序执行将在此处开始并结束。
//

#include <iostream>
#include <string>
#include<opencv2\opencv.hpp>

using namespace std;
using namespace cv;

int main(int argc, char** argv){
	/****************************************	初始化	****************************************************/

	Mat imgIn, imgOut;
	Mat mask;

	imgIn = imread("Test.jpg");
	//imgOut = imgIn;		//证实了这种复制方法只是把in的地址给了out,如果改变out内容,则in也会改变
	imgIn.copyTo(imgOut);		//这种方式会分配新的内存,且会检测需不需要分配新地址
	//imgOut = imgIn.clone();		//这种方法会分配新的内存,且一定会分配新地址

	/****************************************	初始化	****************************************************/





	/****************************************	图像操作	****************************************************/
	int cont = 0;
	int i, j;

	//创建指定Mat
	//imgOut = Mat(100, 100, CV_8UC3, Scalar(0, 0, 0));		//创建全黑图像
	//imgOut = Mat(100, 100, CV_8UC3, Scalar(255, 255, 255));		//创建全白图像

	//像素归零
	//for (j = 0; j < imgOut.rows; j++) {
	//	for (i = 0; i < imgOut.cols*3; i++) {
	//		imgOut.at<uchar>(j, i) = 0;		//at方法相当于在操作矩阵,对于这种三个像素一组的矩阵操作不方便,也是col要乘三的原因;
	//	}
	//}

	//算法创建渐变灰度图(at方法)(防溢出)
	//imgOut = Mat(500, 255, CV_8UC1);
	//uchar gray = 0;
	//for (j = 0; j < imgOut.rows; j++) {
	//	gray = saturate_cast<uchar>(j);
	//	for (i = 0; i < imgOut.cols; i++) {
	//		imgOut.at<uchar>(j, i) = gray;
	//	}
	//}

	//算法创建渐变灰度图(ptr方法)(防溢出)(单通道图像操作)
	//imgOut = Mat(500, 255, CV_8UC1);
	//uchar gray = 0;
	//uchar* index;
	//for (j = 0; j < imgOut.rows; j++) {
	//	gray = saturate_cast<uchar>(j);
	//	for (i = 0; i < imgOut.cols; i++) {
	//		index = imgOut.ptr<uchar>(j, i);
	//		*index = gray;
	//	}
	//}

	//算法创建渐变灰度图(ptr方法)(防溢出)(多通道图像操作)
	imgOut = Mat(255, 255, CV_8UC3, Scalar(0,0,0));
	Vec3b color = {0,0,0};		//与c++的vector类似,可以通用?
	Vec3b* index;
	for (j = 0; j < imgOut.rows; j++) {
		for (i = 0; i < imgOut.cols; i++) {
			color = { saturate_cast<uchar>(j),saturate_cast<uchar>(i) ,0 };
			index = imgOut.ptr<Vec3b>(j, i);
			*index = color;
		}
	}
	/****************************************	图像操作	****************************************************/





	/****************************************	图像输出	****************************************************/
	namedWindow("input", WINDOW_AUTOSIZE);
	imshow("input", imgIn);
	namedWindow("output", WINDOW_AUTOSIZE);
	imshow("output", imgOut);

	//cout << "Mat=" << endl << imgOut << endl;

	/****************************************	图像输出	****************************************************/



	waitKey(0);
	return 0;
}

// 运行程序: Ctrl + F5 或调试 >“开始执行(不调试)”菜单
// 调试程序: F5 或调试 >“开始调试”菜单

// 入门使用技巧: 
//   1. 使用解决方案资源管理器窗口添加/管理文件
//   2. 使用团队资源管理器窗口连接到源代码管理
//   3. 使用输出窗口查看生成输出和其他消息
//   4. 使用错误列表窗口查看错误
//   5. 转到“项目”>“添加新项”以创建新的代码文件，或转到“项目”>“添加现有项”以将现有代码文件添加到项目
//   6. 将来，若要再次打开此项目，请转到“文件”>“打开”>“项目”并选择 .sln 文件

```


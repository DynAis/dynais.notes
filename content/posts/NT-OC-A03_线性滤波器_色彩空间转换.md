---
title: OpenCV学习笔记03-线性滤波器-色彩空间转换
tags:
  - OpenCV
  - 数字图像处理
categories:
  - 笔记
  - OpenCV
keywords:
- opencv
- 线性滤波器
- 色彩空间转换
- cvtColer
thumbnailImage: https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200724212717.png
thumbnailImagePosition: 
coverImage: https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725004705.jpg
coverMeta: in
coverSize: partial
metaAlignment: center
abbrlink: a5f2a55c
date: 2020-01-21 00:00:00
---

### 完成

- 统计时间
- 色彩空间转换
- 线性滤波器使用
- 图像读取写入plus
- 图像指针



### 相关函数

```c++
gettickcount();//获取时钟
mat.ptr<uchar>;//获取图像指针
saturate_cast<uchar>;//防溢出函数
filter2D;//线性滤波器
imread();
imwrite();
cvtColer();//色彩空间转换
```
<!-- more -->


### 实现

**使用卷积加强图像对比度**



### 笔记

- **关于imread和imwrite的地址传入**

  可以使用c++的string或cv自己的String实现,使用cin读入地址



### 源

```c++
// OpenCV_Template.cpp : 此文件包含 "main" 函数。程序执行将在此处开始并结束。
//

#include <iostream>
#include <string>
#include<opencv2\opencv.hpp>

using namespace std;
using namespace cv;

void colChange(Mat &iImg, Mat &oImg) {	//色彩空间变换
	cvtColor(iImg, oImg, COLOR_BGR2GRAY);
	return;
}

void addFilter(Mat &iImg, Mat &oImg,const Mat filter) {	//添加线性滤波器
	filter2D(iImg, oImg, -1, filter);
	return;
}

int main(int argc, char** argv)		//实现读取摄像头内容输出加强对比度,并统计每帧处理时间
{
	VideoCapture cap(0);
	if (!cap.isOpened())
		return -1;
    
	//namedWindow("frame", WINDOW_AUTOSIZE);
	//while(1)
	/*{
		Mat frameIn;
		cap >> frameIn;*/
	//	imshow("frame", frameIn);
	//	if (waitKey(30) >= 0)
	//		break;
	//}

    
    
	Mat iImg;
	Mat oImg;
	Mat filter ;
	String path1;
	string path2;


	
	//cin >> path1;
	//path2 = path1;

	//iImg = imread(path2);
	//if (iImg.empty()) {
	//	printf("Can not read img...");
	//	return -1;
	//}
	while (1) {
		cap >> iImg;
		oImg = Mat::zeros(iImg.size(), iImg.type());	//创建零矩阵
		filter = (Mat_<char>(3, 3) << 0, -1, 0, -1, 5, -1, 0, -1, 0);	//定义卷积核



		double tCount = 0;
		tCount = getTickCount();

		//colChange(iImg, oImg);
		addFilter(iImg, oImg, filter);
		//iImg = imread("Test.jpg", IMREAD_GRAYSCALE);
		//oImg = iImg;

		double tSum = 0;
		tSum = (getTickCount() - tCount) / getTickFrequency();
		printf("Time consume %.4f", tSum);



		//imwrite("layout.jpg", oImg);
		namedWindow("imput", WINDOW_AUTOSIZE);
		imshow("imput", iImg);
		namedWindow("layout", WINDOW_AUTOSIZE);
		imshow("layout", oImg);
		if (waitKey(30) >= 0) {
			break;
		};
	}
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



### 相关

无


---
title: OpenCV学习笔记05-各类模糊
tags:
  - OpenCV
  - 数字图像处理
categories:
  - 笔记
  - OpenCV
keywords:
- opencv
- blur
thumbnailImage: https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200724212717.png
thumbnailImagePosition: 
coverImage: https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725004705.jpg
coverMeta: in
coverSize: partial
metaAlignment: center
abbrlink: 84d10aa8
date: 2020-01-29 00:00:00
---


### 相关函数

```c++
blur();		//均值模糊
GaussianBlur();		//高斯模糊
medianBlur();		//中值滤波
bilateralFilter()		//双边滤波

```



### 实现

- 模糊
  
  - 均值滤波
  - 高斯滤波
  - 中值滤波
  - 双边滤波
        
  


### 笔记

- **高斯滤波是通过高斯函数也就是正态分布来给mask权重**
- sigma越大正态分布上表现就是越平滑

<!-- more -->

- **中值滤波是统计排序滤波器,对椒盐噪声有很好的抑制作用**
- **注意区分中值和均值**




 - 高斯模糊没有考虑像素值的差异,会导致边缘还是不那么清晰
 - **引入空间域核与值域核考虑,空间域就相当于普通的高斯滤波,根据相邻距离决定权重,而值域核是由目标像素值与中心像素值差来给定权重**
 - 简单来说就是双边模糊对高斯模糊来说多了一层mask,这层mask不是根据像素空间位置来给定权重的,而是根据像素与中心像素值之差得出
 - **双边滤波可以磨皮(**



- 剩下的看注释


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
	if (imgIn.empty()) {
		cout << "Can not open this IMG..." << endl;
		return -1;
	}
	imgOut = imgIn.clone();

	/****************************************	初始化	****************************************************/





	/****************************************	图像操作	****************************************************/
	//blur(imgIn, imgOut, Size(9, 9), Point(-1, -1));		//均值模糊

	Mat imgOut2;
	//double sigma = 3;
	//GaussianBlur(imgIn, imgOut2, Size(9,9), sigma, sigma);		//高斯模糊

	Mat imgOut3;
	//medianBlur(imgIn, imgOut3, 9);		//中值滤波

	Mat imgOut4;
	bilateralFilter(imgIn, imgOut, 15, 30.0, 30.0);
	bilateralFilter(imgIn, imgOut2, 30, 30.0, 30.0);		//在sigmaColor很大的情况下,修改sigmaSpace效果很小
	bilateralFilter(imgIn, imgOut3, 50, 30.0, 30.0);		//sigmaColor越大,色块化越严重
	bilateralFilter(imgIn, imgOut4, 100, 30.0, 30.0);		//范围d越大,柔化越明显




	/****************************************	图像操作	****************************************************/





	/****************************************	图像输出	****************************************************/
	namedWindow("input", WINDOW_NORMAL);
	imshow("input", imgIn);
	namedWindow("output", WINDOW_NORMAL);
	imshow("output", imgOut);
	namedWindow("output2", WINDOW_AUTOSIZE);
	imshow("output2", imgOut2);
	namedWindow("output3", WINDOW_AUTOSIZE);
	imshow("output3", imgOut3);
	namedWindow("output4", WINDOW_AUTOSIZE);
	imshow("output4", imgOut4);

	//imwrite("D:/Download/Family2020_Final.jpg", imgOut);
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
	if (imgIn.empty()) {
		cout << "Can not open this IMG..." << endl;
		return -1;
	}
	imgOut = imgIn.clone();

	/****************************************	初始化	****************************************************/





	/****************************************	图像操作	****************************************************/
	//blur(imgIn, imgOut, Size(9, 9), Point(-1, -1));		//均值模糊

	Mat imgOut2;
	//double sigma = 3;
	//GaussianBlur(imgIn, imgOut2, Size(9,9), sigma, sigma);		//高斯模糊

	Mat imgOut3;
	//medianBlur(imgIn, imgOut3, 9);		//中值滤波

	Mat imgOut4;
	bilateralFilter(imgIn, imgOut, 15, 30.0, 30.0);
	bilateralFilter(imgIn, imgOut2, 30, 30.0, 30.0);		//在sigmaColor很大的情况下,修改sigmaSpace效果很小
	bilateralFilter(imgIn, imgOut3, 50, 30.0, 30.0);		//sigmaColor越大,色块化越严重
	bilateralFilter(imgIn, imgOut4, 100, 30.0, 30.0);		//范围d越大,柔化越明显




	/****************************************	图像操作	****************************************************/





	/****************************************	图像输出	****************************************************/
	namedWindow("input", WINDOW_NORMAL);
	imshow("input", imgIn);
	namedWindow("output", WINDOW_NORMAL);
	imshow("output", imgOut);
	namedWindow("output2", WINDOW_AUTOSIZE);
	imshow("output2", imgOut2);
	namedWindow("output3", WINDOW_AUTOSIZE);
	imshow("output3", imgOut3);
	namedWindow("output4", WINDOW_AUTOSIZE);
	imshow("output4", imgOut4);

	//imwrite("D:/Download/Family2020_Final.jpg", imgOut);
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


---
title: OpenCV学习笔记09-Canny边缘检测算法
tags:
  - OpenCV
  - 数字图像处理
categories:
  - 笔记
  - OpenCV
keywords:
- opencv
- canny
- 边缘检测
thumbnailImage: https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200724212717.png
thumbnailImagePosition: 
coverImage: https://dynais-imh-hub.oss-cn-hangzhou.aliyuncs.com/img/20200725004705.jpg
coverMeta: in
coverSize: partial
metaAlignment: center
abbrlink: 80e5fe0
date: 2020-02-16 20:00:00
---

### API

```c++
Canny();	//Canny的API, 包含了4个步骤. 注意, 不包含高斯模糊部分
```



### 笔记

- **Canny边缘检测算法可以分为以下5个步骤：**

  -  使用高斯滤波器，以平滑图像，滤除噪声。(需要调用高斯模糊API)

  -  计算图像中每个像素点的梯度强度和方向。

  - 应用非极大值（Non-Maximum Suppression）抑制，以消除边缘检测带来的杂散响应。

  - 应用双阈值（Double-Threshold）检测来确定真实的和潜在的边缘。

  -  通过抑制孤立的弱边缘最终完成边缘检测。



- **非极大值抑制:**

细化边缘, 但技术的实现细节并不是很懂, 大致思想是取邻域中的梯度极大值点来进行有效边缘的判断, 下面的文章讲的很详细, 可以看看.

<!-- more -->

- **关于几种边缘检测方法:**

Laplance, Canny 和 Sobel 都是边缘检测的方法, Canny是包含了Sobel算子的边缘检测, 所以可以说是Sobel的实际应用, Laplance的检测效果并不好, 但是有其他的用途, 总的来说Canny能应对大多数的场景




### 参考来源

- 《A Computational Approach to Edge Detection》

- [1]: https://www.cnblogs.com/techyan1990/p/7291771.html	"边缘检测之Canny"

  

### 源//对NXP赛道进行下采样和边缘检测

```c++
// OpenCV_Template.cpp : 此文件包含 "main" 函数。程序执行将在此处开始并结束。
//

#include <iostream>
#include <string>
#include<opencv2\opencv.hpp>

using namespace std;
using namespace cv;

Mat imgIn, imgOut;

int main(int argc, char** argv) {
	/****************************************	初始化	****************************************************/

	imgIn = imread("D:/WorkSpace/Projects/OpenCV Learning/ImageHub/直道进圆环.jpg", IMREAD_COLOR);
	if (imgIn.empty()) {
		cout << "Can not open this IMG..." << endl;
		return -1;
	}

	//VideoCapture(0) >> imgIn;
	imgOut = imgIn.clone();

	/****************************************	初始化	****************************************************/





	/****************************************	图像操作	****************************************************/
	double tCount = 0;
	double tSum = 0;
	tCount = getTickCount();

	cvtColor(imgIn, imgOut, COLOR_BGR2GRAY);//Canny只接受8位深度的灰度图
	pyrDown(imgOut, imgOut, Size(imgOut.cols / 2, imgOut.rows / 2));//下采样
	pyrDown(imgOut, imgOut, Size(imgOut.cols / 2, imgOut.rows / 2));
	pyrDown(imgOut, imgOut, Size(imgOut.cols / 2, imgOut.rows / 2));
	//GaussianBlur(imgOut, imgOut, Size(3, 3), 1.4);

	Canny(imgOut, imgOut, 50, 125, 3);//第三,四个参数代表上下阈值, 第五个是Sobel算子的大小, 一般取3

	tSum = (getTickCount() - tCount) / getTickFrequency();
	printf("Time consume %.4f\n\n", tSum);


	/****************************************	图像操作	****************************************************/





	/****************************************	图像输出	****************************************************/
	namedWindow("input", WINDOW_NORMAL);
	imshow("input", imgIn);
	namedWindow("output", WINDOW_AUTOSIZE);
	imshow("output", imgOut);
	waitKey(0);
	//cout << imgOut << endl;
}
	/****************************************	图像输出	****************************************************/

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


---
title: '[CV] 形态学操作'
tags:
  - OpenCV
date: 2020-01-30
---

### 相关函数

```c++
getStructuringElement(int shape, Size ksize ,Point anchor);注意size还是要奇数
dilate(src, dst, kernel);膨胀
erode(src, dst, kernel);腐蚀
creatTrackbar();创建滑块,比较实用,但我搞不懂

morphologyEX();形态学操作

adaptiveThreshold();
threshold(); //大津法

```



### 实现

- 膨胀
- 腐蚀
- 开操作 
- 形态学梯度



- 提取垂直或水平的线(使用水平或竖直的结构体)
- 二值化
- 对图像取反(用~)

<!-- more -->

### 笔记

- opencv结构元素获取(getStructuringElement)我理解是类似卷积核的东西
- 膨胀:区域最大值覆盖中心值
- 腐蚀:区域最小值覆盖中心值



- 开操作:先腐蚀后膨胀,去掉小的对象
- 闭操作:先膨胀后腐蚀,填充小的洞
- 形态学梯度可以方便得提取边线
- 提取垂直或水平的线思路: 使用特殊的结构体来提取特殊的结构,比如一条横线进行开操作就可以提取出横线结构(操作完以后可以blur一下) 
- 在进行阙值分割前对图像进行模糊处理(图像处理领域好像叫滤波?)再分割貌似有更好的效果
- 挑战: 验证码识别


### 相关

无

### 源

主要是滑块的应用

```c++
// OpenCV_Template.cpp : 此文件包含 "main" 函数。程序执行将在此处开始并结束。
//

#include <iostream>
#include <string>
#include<opencv2\opencv.hpp>

using namespace std;
using namespace cv;

Mat structs;
Mat imgIn, imgOut;
const int MAXSIZE = 30;
int size_ = 0;

void Graph(int,void*);

int main(int argc, char** argv){
	/****************************************	初始化	****************************************************/
	//VideoCapture cap;
	//cap = VideoCapture(0);
	//Mat cap0;
	//VideoCapture(0) >> cap0;
	//imshow("test", cap0);

	imgIn = imread("D:/WorkSpace/Projects/OpenCV学习/ImageHub/Code1.png", IMREAD_GRAYSCALE);
	if (imgIn.empty()) {
		cout << "Can not open this IMG..." << endl;
		return -1;
	}

	//imgIn = cap0.clone();
	//cvtColor(imgIn, imgIn, COLOR_BGR2GRAY);
	//imshow("test", imgIn);

	medianBlur(imgIn, imgIn, 5);

	//threshold(~imgIn, imgIn, 0, 255, THRESH_OTSU);
	adaptiveThreshold(~imgIn, imgIn, 255, ADAPTIVE_THRESH_GAUSSIAN_C, THRESH_BINARY, 33, -10);

	imgOut = imgIn.clone();

	/****************************************	初始化	****************************************************/





	/****************************************	图像操作	****************************************************/
	namedWindow("output", WINDOW_NORMAL);
	imshow("output", imgOut);
	createTrackbar("Kern Size", "output", &size_, MAXSIZE, Graph);		//这个函数调用的方法非常奇特我搞不懂为什么,前两句是为了初始化窗口↑,注意最后一个参数虽然是函数但是不用括号

	/****************************************	图像操作	****************************************************/





	/****************************************	图像输出	****************************************************/
	//namedWindow("input", WINDOW_AUTOSIZE);
	//imshow("input", imgIn);
	//namedWindow("output2", WINDOW_AUTOSIZE);
	//imshow("output2", imgOut2);
	//namedWindow("output3", WINDOW_AUTOSIZE);
	//imshow("output3", imgOut3);
	//namedWindow("output4", WINDOW_AUTOSIZE);
	//imshow("output4", imgOut4);

	//imwrite("D:/Download/Family2020_Final.jpg", imgOut);
	//cout << "Mat=" << endl << imgOut << endl;

	/****************************************	图像输出	****************************************************/



	waitKey(0);
	return 0;
}



void Graph(int, void*) {		//注意书写格式,虽然我不知道为什么

	int s = size_ * 2 + 1 ;
	structs = getStructuringElement(MORPH_RECT, Size(s, s), Point(-1, -1));

	//erode(imgIn, imgOut, structs);
	//dilate(imgOut, imgOut, structs);

	morphologyEx(imgIn, imgOut, MORPH_GRADIENT, structs);

	imshow("output", imgOut);

	return;
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


---
title: '[CV] 图像混合-亮度对比度-几何绘制'
tags:
  - OpenCV
date: 2020-01-25
---

### 相关函数

```c++
mat.at<xxx>
bitwise_not();//反色
src.convertTo();//通道转换

addWeighted()//图像混合加权相加,大小类型必须一致
multiply()//图像相乘

Mat::zeros

cv:point
cv:scalar
line();
cv:rect
rectangle();

```



### 实现

- 对像素的操作
- 图像混合    
- 对比度和亮度调节    
- 几何绘制(人脸追踪框可能)

<!-- more -->

### 笔记

- **通过权重相加函数实现图像混合效果**

```c++
addWeighted()
```

- **对比度和亮度调节的实现思想**
  - **像素值相乘**(对比度实现,因为拉大了数值差)  
  - **像素值加常数**(亮度实现)   
  - **公式**:g(x,y) = alpha * f(x,y) + beta


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
	//cout << imgOut.at<Vec3b>(20, 20) << endl;
	//printf("%d\n", imgOut.at<Vec3b>(20, 20)[0]);


	bitwise_not(imgIn, imgOut);		//图像混合
	Mat output(imgIn.size(), imgIn.type());
	addWeighted(imgIn, 0.6, imgOut, 0.4, 0.0, output);
	

	Rect pos(200, 200, 200, 200);		//画框
	rectangle(output, pos, Scalar(255, 0, 0), 1, LINE_8, 0);


	int ix, iy;
	//int col = imgIn.cols;
	//int row = imgIn.rows;
	for (ix = 0; ix < imgIn.cols; ix++) {
		for (iy = 0; iy < imgIn.rows; iy++) {
			for (int channal = 0; channal < 3; channal++) {
				output.at<Vec3b>(ix, iy)[channal] = saturate_cast<uchar>(output.at<Vec3b>(ix, iy)[channal] * 3 - 190);		//对每个像素的通道进行计算,三倍单位对比度,-190等亮度
			}
		}
	}
	/****************************************	图像操作	****************************************************/





	/****************************************	图像输出	****************************************************/
	namedWindow("input", WINDOW_AUTOSIZE);
	imshow("input", imgIn);
	namedWindow("output", WINDOW_AUTOSIZE);
	imshow("output", output);

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


---
title: "[CV] 霍夫线和圆检测"
tags:
  - OpenCV
date: 2020-02-16
---

### API

```c++
/*霍夫线检测 输入图像要先Canny过 参数为
- 输入图像
- 输出向量数组,数据类型为Vec4i(就是两个点)
- 默认1
- 默认CV_PI / 180, 转角步长
- 阈值(我设了100)
- 最小线长
- 最大间隙, 小于这个值的两条线会连成一条, 对于断断续续的线效果好
*/
void HoughLinesP( InputArray image, OutputArray lines,
                 double rho, double theta, int threshold,
                 double minLineLength = 0, double maxLineGap = 0 );


/*霍夫圆检测 参数从前往后分别是
- 输入图像矩阵(8bit的灰度图,这个API自带Canny边缘检测)
- 输出向量数组,数据类型位Vec3f
- HOUGH_GRADIENT

- 图像缩放,默认1
- 圆心最小距离, 小于会认为是同心圆?
- Canny检测的大阈值,小的=大的除二计算
- 点重叠n个以上判定为圆,越小检出越多圆
- 最小圆半径
- 最大圆半径
*/
void HoughCircles( InputArray image, OutputArray circles,
                  int method, double dp, double minDist,
                  double param1 = 100, double param2 = 100,
                  int minRadius = 0, int maxRadius = 0 );


```

<!-- more -->

### 笔记

- 圆检测对噪声敏感, 需要先中值滤波
- 太难了,建议看下面的博客,线检测还好,圆检测真的看不懂


### 相关

[1]: https://www.cnblogs.com/php-rearch/p/6760683.html	"霍夫变换"



### 源//检出NXP赛道上的几何图

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

	cvtColor(imgIn, imgIn, COLOR_BGR2GRAY);
	pyrDown(imgIn, imgIn, Size(imgIn.cols / 2, imgIn.rows / 2));
	pyrDown(imgIn, imgIn, Size(imgIn.cols / 2, imgIn.rows / 2));
	pyrDown(imgIn, imgIn, Size(imgIn.cols / 2, imgIn.rows / 2));
	//GaussianBlur(imgOut, imgOut, Size(3, 3), 1.4);

	//霍夫圆检测
	imgOut = Mat::zeros(imgIn.size(), imgIn.type());
	vector<Vec3f> circles;
	HoughCircles(imgIn, circles, HOUGH_GRADIENT, 1, 50, 125, 30);//参数很难试
	Vec3f aCircle;
	for (size_t i = 0; i < circles.size(); i++) {
		aCircle = circles[i];
		circle(imgOut, Point(aCircle[0],aCircle[1]), aCircle[2], Scalar(255), 1, LINE_AA);
	}

	//霍夫直线检测
	vector<Vec4i> lines;
	Canny(imgIn, imgIn, 50, 125, 3);
	HoughLinesP(imgIn, lines, 1, CV_PI / 180, 60, 0.0, 20.0);

	Vec4i aLine;
	for (size_t i = 0; i < lines.size(); i++) {
		aLine = lines[i];
		line(imgOut, Point(aLine[0], aLine[1]), Point(aLine[2], aLine[3]) ,Scalar(255), 1, LINE_AA);
	}

	tSum = (getTickCount() - tCount) / getTickFrequency();
	printf("Time consume %.4f\n\n", tSum);


	/****************************************	图像操作	****************************************************/





	/****************************************	图像输出	****************************************************/
	namedWindow("input", WINDOW_AUTOSIZE);
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


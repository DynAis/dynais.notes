---
title: "[CV] 模版匹配"
tags:
  - OpenCV
date: 2020-02-20
---


### API

```c++
matchTemplate();//模式查找,API比较简单
minMaxLoc();//用于在模式查找的输出图像中找到极值点,也就是匹配点
```



### 笔记

- 模板匹配(Templet Match)

  相当于上一节说的直方图匹配的实用化,通过现有图像在目标图像上滑行(原文Slide),也就是左到右上到下的以像素为单位进行匹配,找到匹配值最大的点.但也是因为这个原因,对模板图像和在目标图像里的目标的大小进行匹配就非常重要,如果大小差得远,效果就不好,所以使用条件相当苛刻.



- 注意输出图像的大小

  在API中需要提供一个储存输出结果的Mat, 他的大小是

  ```
  Size(src.cols-templ.cols+1, src.rows-templ.rows+1)
  ```

<!-- more -->

- OpenCV的查找模式

  OpenCV提供了很多种方法,在官网上都有介绍,大部分都是取用了最大值作为最匹配

  根据最小值匹配的只有 **TM_SQDIFF** 和 **MT_SQDIFF_NORMED**

  *For the first two methods ( TM_SQDIFF and MT_SQDIFF_NORMED ) the best match are the lowest values.*

  

- OpenCV中32位的图像

  每个数值是一个位于[0,1]间的小数,相当于8位的[0,255]



---------------------------



### 源//API实现模式查找

```c++
// OpenCV_Template.cpp : 此文件包含 "main" 函数。程序执行将在此处开始并结束。
//

#include <iostream>
#include<opencv2\opencv.hpp>

using namespace std;
using namespace cv;

Mat src, dst, temp;

int main(int, char**)
{
	temp = imread("D:/WorkSpace/Projects/OpenCV Learning/ImageHub/Lena.jpg");
	src = imread("D:/WorkSpace/Projects/OpenCV Learning/ImageHub/Day1.png");

	//测试尺度不变性
	//pyrDown(temp, temp, Size(temp.cols / 2, temp.rows / 2));
	pyrUp(temp, temp, Size(temp.cols * 2, temp.rows * 2));
	//pyrUp(temp, temp, Size(temp.cols * 2, temp.rows * 2));

	if (temp.empty() || src.empty()) {
		cout << "Can not open this IMG... Check again!";
		return -1;
	}

	Mat result = Mat_<float>::zeros(src.cols - temp.cols + 1, src.rows - temp.rows + 1 );

	matchTemplate(src, temp, result, TM_CCOEFF_NORMED);

	//cout << result;

	double minVal; double maxVal; Point minLoc; Point maxLoc;
	Point matchLoc;
	minMaxLoc(result, &minVal, &maxVal, &minLoc, &maxLoc, Mat());
	cout << minVal << endl << maxVal << endl << minLoc << endl << maxLoc << endl;
	rectangle(src, maxLoc, Point(maxLoc.x + temp.cols, maxLoc.y + temp.rows), Scalar(0,0,255), 2, 8);
	rectangle(result, Point(maxLoc.x - temp.cols/2, maxLoc.y - temp.rows/2), Point(maxLoc.x + temp.cols/2, maxLoc.y + temp.rows/2), Scalar::all(1), 2, 8, 0);

	namedWindow("src", WINDOW_AUTOSIZE);
	pyrDown(src, src, Size(src.cols / 2, src.rows / 2));
	pyrDown(src, src, Size(src.cols / 2, src.rows / 2));
	imshow("src", src);
	namedWindow("result", WINDOW_AUTOSIZE);
	pyrDown(result, result, Size(result.cols / 2, result.rows / 2));
	pyrDown(result, result, Size(result.cols / 2, result.rows / 2));
	imshow("result", result);

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


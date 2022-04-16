---
title: '[CV] 直方图均衡化-直方图比较-反向投影'
tags:
  - OpenCV
date: 2020-02-19
---


### API

```c++
- equalizeHist();//直方图均衡化
- split();//分离通道
- calcHist();//参数dims,bin,range
- waitkey();

- mixChannels//分离通道, 与split小有差别,建议看官方文档
- cvtColer//使用此api转换到hsv色彩空间
- calcHist//接受单通道图像计算直方图, 参数略微复杂
- normalize//归一化,常用
- compareHist//比较直方图,可以得到两张图片的相似程度,但是对光非常敏感
- backProject();//直方图反向投影

```



### 笔记

*这里是几个关于直方图的总结, 这一堆实在是不太好懂, 并且映射和统计接触到了很多数学方面的东西,重要的是理解思路以及了解API, 这里的东西要是有不理解的都建议去看官方的教程文档*

[1]: https://docs.opencv.org/master/d8/dc8/tutorial_histogram_comparison.html	"官方文档-直方图比较"

<!-- more -->

- **直方图均衡化**

好像在人脸识别的项目总结里写过了, API并不难理解



- **HSV模型**

HSV是一种比较直观的颜色模型，所以在许多图像编辑工具中应用比较广泛，这个模型中颜色的参数分别是：色调（H, Hue），饱和度（S,Saturation），明度（V, Value）



- **直方图比较**

```c++
compareHist();
```

API比较方便,输入两个直方图,比较他们的相似程度

**这两个直方图通常会是图像的HS直方图**(虽然我现在还不太懂HS为什么可以变成一张直方图,到时候要用再看原理好了),用HS猜测是要降低算法对光线的敏感度?(实测好像对光线还是很敏感)

OpenCV提供了一共四种方法

- 相关性计算:{-1, 1}  //1最强
- 卡方计算:{0, ∞}  //0最强
- 十字交叉
- 巴氏距离计算:{0, 1}  //0最强

其中比较推荐的是相关性计算和巴氏距离计算(不需要归一化了hhhhhhhhh)

数学公式不列出了(反正我又不会去看)



- **直方图反向投影**

[^0]: 论文:《Indexing Via Color Histograms》

```
mixChannels();
backProject();
```



直方图反向投影是一种基于色彩的对象识别技术,通过该方法可以定位图像中已知物体的位置,反应直方图在目标图像中的分布

主要思路是提取已知图像的Hue(色相)空间,做出直方图,再反向找到这些色相在目标图片中的分布,已知图像中越多的色相,在backProject中就会(看起来)更亮,利用这点加上一些二值化,就可以得到一张目标物体的掩膜,覆盖到目标图片上就可以得到完成的图像了,如下





----------------------------------------



### 源//读取TIM图标, 在桌面截图上找到他

```c++
// OpenCV_Template.cpp : 此文件包含 "main" 函数。程序执行将在此处开始并结束。
//

#include "opencv2/imgproc.hpp"
#include "opencv2/imgcodecs.hpp"
#include "opencv2/highgui.hpp"
#include <iostream>


using namespace cv;
using namespace std;

Mat hue;
Mat target_hue;
int bins = 25;
Mat src_mask_globle;
Mat target;

void Hist_and_Backproj(int, void*);

int main(int argc, char* argv[])
{
    //读入src
    CommandLineParser parser(argc, argv, "{@input |D:/WorkSpace/Projects/OpenCV Learning/ImageHub/Tim.png  | input image}");
    Mat src = imread(parser.get<String>("@input"));
    if (src.empty())
    {
        cout << "Could not open or find the image!\n" << endl;
        cout << "Usage: " << argv[0] << " <Input image>" << endl;
        return -1;
    }
    
    target = imread("D:/WorkSpace/Projects/OpenCV Learning/ImageHub/屏幕.png");
    pyrDown(target, target, Size(target.cols / 2, target.rows / 2));
    pyrDown(target, target, Size(target.cols / 2, target.rows / 2));
    //pyrDown(src, src, Size(src.cols / 2, src.rows / 2));

    //二值化取覆膜
    Mat src_gray;
    cvtColor(src, src_gray, COLOR_BGR2GRAY);
    Mat src_mask;
    threshold(src_gray, src_mask, 0, 255, THRESH_TRIANGLE);
    src_mask_globle = src_mask;
    imshow("BinMask", src_mask);

    //色彩空间转换
    //src = Mat(src.size(), src.type(), Scalar(255, 0, 0));
    Mat hsv;
    cvtColor(src, hsv, COLOR_BGR2HSV);
    Mat target_hsv;
    cvtColor(target, target_hsv, COLOR_BGR2HSV);

    //创建Hue空间通道图像
    hue.create(hsv.size(), hsv.depth());
    target_hue.create(target_hsv.size(), target_hsv.depth());
    int ch[] = { 0, 0 };
    mixChannels(&hsv, 1, &hue, 1, ch, 1);
    mixChannels(&target_hsv, 1, &target_hue, 1, ch, 1);
    //cout << hue;

    //创建滑块并BackProjection
    const char* window_image = "Source image";
    namedWindow(window_image);
    createTrackbar("* Hue  bins: ", window_image, &bins, 180, Hist_and_Backproj);
    Hist_and_Backproj(0, 0);
    imshow(window_image, src);

    // Wait until user exits the program
    waitKey(0);

    return 0;
}

void Hist_and_Backproj(int, void*)
{
    //防止bins太小
    int histSize = MAX(bins, 2);

    //计算Hue空间直方图
    float hue_range[] = { 0, 180 };
    const float* ranges = { hue_range };
    Mat hist;
    calcHist(&hue, 1, 0, src_mask_globle, hist, 1, &histSize, &ranges, true, false);
    normalize(hist, hist, 0, 255, NORM_MINMAX, -1, Mat());

    //BackProjection
    Mat backproj;
    calcBackProject(&target_hue, 1, 0, hist, backproj, &ranges, 1, true);
    threshold(backproj, backproj, 0, 255, THRESH_OTSU);
    imshow("BackProj", backproj);

    //绘制直方图
    int w = 400, h = 400;
    int bin_w = cvRound((double)w / histSize);
    Mat histImg = Mat::zeros(h, w, CV_8UC3);
    for (int i = 0; i < bins; i++)
    {
        rectangle(histImg, Point(i * bin_w, h), Point((i + 1) * bin_w, h - cvRound(hist.at<float>(i) * h / 255.0)),
            Scalar(0, 0, 255), FILLED);
    }
    imshow("Histogram", histImg);

    Mat focus;
    target.copyTo(focus, backproj);
    imshow("focus", focus);
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


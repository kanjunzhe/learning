# OpenCV
---

## 1.图像入门

### 源代码
```c++
#include <opencv2/core.hpp>
#include <opencv2/imgcodecs.hpp>
#include <opencv2/highgui.hpp>
#include <iostream>

using namespace cv;

int main()
{
	std::string image_path = samples::findFile("starry_night.jpg");
	Mat img = imread(image_path, IMREAD_COLOR);
	if (img.empty)
	{
		std::cout << "Could not read the image: " << image_path << std::endl;
		return 1;
	}
	imshow("Display window", img);
	int k = waitKey(0);
	if(k == 's')
	{
		imwrite("starry_night.png", img);
	}
	return 0;
}
```

### 1.命名空间
- [Core](https://docs.opencv.org/3.4/d0/de1/group__core.html) 模块，定义了库的基本构建块 `<opencv2/core.hpp>`
- [Imgcodecs](https://docs.opencv.org/3.4/d4/da8/group__imgcodecs.html) 模块，提供读写功能 `<opencv2/imgcodecs.hpp>`
- [Highgui](https://docs.opencv.org/3.4/d7/dfc/group__highgui.html) 模块，包含显示图像的功能 `<opencv2/highgui.hpp>`
- 我们还导入 _iostream_ 以方便控制台线路输出和输入 `<iostream>`
- 命名空间 `using namespace cv;`
```c++
#include <opencv2/core.hpp>
#include <opencv2/imgcodecs.hpp>
#include <opencv2/highgui.hpp>
#include <iostream>
using namespace cv;
```

### 2.主代码

#### 读取图像
作为第一步，我们从OpenCV样本中读取图像 `starry_night.jpg`
为此，对 `cv::imread` 函数的调用使用第一个参数指定的文件路径加载图像。第二个参数是可选的，它指定我们想要图像的格式。这可能是：
- `IMREAD_COLOR` 以 BGR 8 位格式加载图像。这是此处使用的 **默认值**
- `IMREAD_UNCHANGED` 按原样加载图像（包括 `Alpha` 通道，如果存在）
- `IMREAD_GRAYSCALE` 将图像加载为强度

读取后的图像存放在 `cv::Mat` 对象中
```c++
std::string image_path = samples::findFile("starry_night.jpg");
Mat img = imread(image_path, IMREAD_COLOR);
```

#### $\color {red} {注 意 }$
OpenCV支持图像格式`bmp`，`pbm`，`pgm`，`ppm`，`sr`，`ras`。在插件的帮助下（如果自己构建库，需要指定使用它们），但在我们默认提供的软件包中还可以加载图像格式，如 `jpeg`，`jpg`，`jpe`，`jpeg2000`（jp2 - 在 CMake 中代号为 Jasper），TIFF 文件（`tiff`，`tif`）和`png`

#### 加载检查
```c++
if(img.empty())
{
	std::cout << "Could not read the image: " << image_path << std::endl;
	return 1;
}
```

#### 图像显示
imshow：使用对 [cv::imshow](https://docs.opencv.org/3.4/d7/dfc/group__highgui.html#ga453d42fe4cb60e5723281a89973ee563) 函数的调用来显示图像。第一个参数是窗口的标题，第二个参数是将显示的 [cv::Mat](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html) 对象
waitkey：因为我们希望我们的窗口一直显示到用户按下一个键（否则程序会结束得太快），所以我们使用 [cv::waitKey](https://docs.opencv.org/3.4/d7/dfc/group__highgui.html#ga5628525ad33f52eab17feebcfba38bd7) 函数，其唯一的参数是它应该等待用户输入多长时间（以毫秒为单位，零意味着永远等待），返回值是按下的键
```c++
imshow("Display window", img);
int k = waitKey(0);
```

#### 写入文件
如果按下的键是“s”键（按键捕获见上），则图像将写入文件。
[cv::imwrite](https://docs.opencv.org/3.4/d4/da8/group__imgcodecs.html#gabbc7ef1aa2edfaa87772f1202d67e0ce "Saves an image to a specified file.") 函数将文件路径和 [cv::Mat](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html "n-dimensional dense array class") 对象作为参数
```c++
if(k == 's')
{
	imwrite("starry_night.png", img);
}
```

## 2.图像进阶-Mat

> ![[Pasted image 20230225192031.jpg]]
> 在上图中，汽车的镜子只不过是一个包含像素点所有像素值的矩阵 

### 复制矩阵
每个 _Mat_ 对象都有自己的标头，但是可以通过让它们的矩阵指针指向同一地址在两个 _Mat_ 对象之间共享矩阵。此外，复制运算符只会复制指向大矩阵的标头和指针，而不是数据本身
```c++
Mat A, C; // 只创建标题部分
A = imread(argv[1], IMREAD_COLOR); // 分配矩阵
Mat B(A); // 使用复制构造函数
C = A; // 赋值运算符
```

上述所有对象都指向同一个数据矩阵，使用其中任何一个进行修改也会影响所有其他对象。实际上，不同的对象只是为相同的基础数据提供不同的访问方法。然而，它们的标题部分是不同的。真正有趣的部分是，可以创建仅引用完整数据子部分的标题。例如，要在图像中创建感兴趣区域（ `ROI` )，只需创建一个具有新边界的新标题
```c++
Mat D (A, Rect(10, 10, 100, 100)); // 使用矩形
Mat E = A(Range::all(), Range(1,3)); // 使用行列边界
```

如果矩阵本身可能属于多个 _Mat_ 对象，当不再需要它时，谁负责清理它？简短的回答是：使用它的最后一个对象。这是通过使用引用计数机制来处理的。每当有人复制 _Mat_ 对象的标头时，都会为矩阵增加一个计数器。每当清理标头时，此计数器都会减少。当计数器达到零时，矩阵被释放。

有时你也想复制矩阵本身，所以OpenCV提供了[clone()](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html#a03d2a2570d06dcae378f788725789aa4)和[copyTo()](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html#a33fd5d125b4c302b0c9aa86980791a77)函数
```c++
Mat F = A.clone();
Mat G;
A.copyTo(G);
```

现在修改 _F_ 或 _G_ 不会影响 _A_ 标头指向的矩阵。需要记住的是：
- OpenCV 函数的输出图像分配是自动的（除非另有说明）
- 您无需考虑使用OpenCV的C++接口进行内存管理
- 赋值运算符和复制构造函数仅复制标头
- 可以使用 [cv::Mat::clone()](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html#a03d2a2570d06dcae378f788725789aa4)  和[cv::Mat::copyTo()](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html#a33fd5d125b4c302b0c9aa86980791a77) 函数复制图像的底层矩阵

### 显式创建 Mat 对象

在加载、修改和保存图像教程中，您已经学习了如何使用 [cv::imwrite()](https://docs.opencv.org/3.4/d4/da8/group__imgcodecs.html#gabbc7ef1aa2edfaa87772f1202d67e0ce) 函数将矩阵写入图像文件。但是，出于调试目的，查看实际值要方便得多。您可以使用 _Mat_ 的<<运算符执行此操作。请注意，这仅适用于二维矩阵。

虽然 _Mat_ 作为图像容器效果很好，但它也是一个通用的矩阵类。因此，可以创建和操作多维矩阵。可以通过多种方式创建 Mat 对象：
```c++
Mat M(2,2, CV_8UC3, Scalar(0,0,255));
cout << "M = " << endl << " " << M << endl << endl;
```
![[img/Pasted image 20230226224455.png]]

然后我们需要指定用于存储元素的数据类型以及每个矩阵点的通道数。为此，我们根据以下约定构建了多个定义：
```c++
CV_[每个项目的位数][有符号或无符号][类型前缀]C[通道号]
```
例如，CV_8UC3意味着我们使用 8 位长的无符号字符类型，每个像素有三个这样的通道来形成三个通道。有为最多四个通道预定义的类型。[cv::Scalar](https://docs.opencv.org/3.4/dc/d84/group__core__basic.html#ga599fe92e910c027be274233eccad7beb)是四元素短向量。指定它，您可以使用自定义值初始化所有矩阵点。如果需要更多，可以使用上部宏创建类型，在括号中设置通道号





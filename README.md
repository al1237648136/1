#调用摄像头 

##使用说明

1. 如何运行这个程序？

   如果你用 Visual Studio：
   - 把main.cpp添加到项目里
   - 配置好OpenCV
   - 按F5运行

2. 需要什么？
   - OpenCV库（版本4.0以上）
   - 一个USB摄像头

3. 常见问题：
   Q: 提示找不到摄像头？
   A: 检查摄像头是否插好，或者试试把 cap(0) 改成 cap(1)
   
   Q: 画面卡住了？
   A: 按ESC退出，重新运行

4. 快捷键：
   ESC - 退出程序

5. 代码说明：
   - 第8行：打开第一个摄像头
   - 第16-25行：相机参数（你的）
   - 第36行：去畸变处理
   - 第39行：显示窗口
   - 第42行：按ESC退出

作者：颜浩文
日期：2026年2月6日

##配置

如何安装OpenCV（超简单版）

========= Windows用户 =========
方法1：最简单（推荐）
1. 下载安装包：https://sourceforge.net/projects/opencvlibrary/
2. 运行安装程序
3. 选择安装路径，比如：C:\opencv
4. 完成

方法2：用vcpkg
1. 打开命令提示符（管理员）
2. 输入：
   git clone https://github.com/Microsoft/vcpkg.git
   cd vcpkg
   bootstrap-vcpkg.bat
   vcpkg install opencv:x64-windows

========= Mac用户 =========
打开终端，输入：
brew install opencv

========= Linux用户 =========
打开终端，输入：
sudo apt-get update
sudo apt-get install libopencv-dev

========= 测试安装 =========
创建一个test.cpp文件：

#include <opencv2/opencv.hpp>
#include <iostream>

int main() {
    std::cout << "OpenCV版本：" << CV_VERSION << std::endl;
    return 0;
}

编译运行，如果显示版本号，就成功了！

========= 需要帮助？ =========
1. 百度搜索：OpenCV安装教程
2. 查看OpenCV官网：https://opencv.org/
3. 问有经验的同学

##代码

#include <opencv2/opencv.hpp>
#include <iostream>
#include <opencv2/imgcodecs.hpp>
#include <opencv2/imgproc.hpp>
#include <opencv2/highgui.hpp>


using namespace cv;
using namespace std;
void main() {
    VideoCapture cap(0);
    Mat img;
    Mat cameraMatrix = (Mat_<double>(3, 3) <<
        327.9305025136076, 0, 305.9181216756677,
        0, 437.6039871995856, 261.8508654836178,
        0, 0, 1);

    Mat distCoeffs = (Mat_<double>(5, 1) <<
        -0.3597320358867337, 0.1105565777290975, -0.007885766130449081,
        0.003370992863840766, 0.02668846321460064);
    while (true) {
        Mat undistorted;
        cap.read(img);        
        undistort(img, undistorted, cameraMatrix, distCoeffs); 
        imshow("image", undistorted);
        waitKey(10);
    }
}





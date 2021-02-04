- [一.环境配置需求](#一环境配置需求)
- [二.程序配置参数](#二程序配置参数)
- [三.程序运行说明](#三程序运行说明)
  - [1.命令行模式](#1命令行模式)
  - [2.Visual Studio Code平台](#2visual-studio-code平台)
语义引导的稠密重建

# 一.环境配置需求
- Ubuntu 18.04
- CGAL 5.0
- OPENCV 3.4.0以上
- eigen 3.0以上
- boost 
- c++ 11
- cmake 3.4以上
- 程序正文请使用GB2312编码格式打开，中文注释才能够正常显示

# 二.程序配置参数
configSL.txt文件内各项参数说明

data_path=/home/xxx/Data/Test 
* 数据路径，需设定

log_name=log 
* 日志文件名，需设定。不设定则不输出日志文件

db_name=Test.db 
* 数据库文件，需设定

image_folder=images 
* 图像文件夹名，默认值为images

sparse_bound_name=sparse_bound.ply 
* 稀疏点云边界文件ply，默认值为sparse_bound.ply

bCreatDB=0  
* 1：name  创建数据库并写入图像文件名
* 2：name+GPS  创建数据库并写入图像文件名，同时写入图像GPS信息（从exif中）

bReadFromFiles=0  
* 1：bundler 从out读取相机SfM信息
* 2：colmap 从colmap文件夹读取相机SfM信息

bSparseBound=0  
* 1：从sSparseBoundName.ply裁剪(convex hull)  
* 2：从sSparseBoundName.ply裁剪(bounding box)  
* 3：根据相机sfm自动裁剪(convex hull)  
* 4：根据相机sfm自动裁剪(bounding box)  
* 5：根据相机GPS自动裁剪(convex hull)  
* 6：根据相机GPS自动裁剪(bounding box)  
* 7：从sSaprsePloygonBoundName.txt裁剪  

bUndistortImage=0  
* 1. 图像畸变矫正

bUndistortLabel=0
* 1. 语义分割图畸变矫正

bNeighborSelection=0  
* 1. 选择邻域图像组

bDepthComputation=0  
* 1. 深度图计算

bDepthFilter=0  
* 1. 深度图过滤

bDepthFusion=0  
* 1. 深度图融合

bDenseBound=0  
* 1：从sDenseBoundName.ply裁剪  
* 2：从sDensePloygonBoundName.txt裁剪  

bColorEstimation=0  
* 1. 点云着色

bPointsLabeling=0    
* 1：点云语义标注，使用点云原始颜色  
* 2：点云语义标注，使用label_color_table.txt设置颜色  

# 三.程序运行说明
语义引导的稠密重建程序主体部分以V1.6.2为基础，更新了以下两个文件：

- 算法程序：/Algo/Algorithms.cpp

- 基本数据结构和函数声明：/base.h

运行可在以下两种方式中任选一种：

## 1.命令行模式
```cpp
//首先切换到程序根目录
cd build
cmake ..
make -j8
./3DMapSL /数据集目录地址/configSL.txt
```

## 2.Visual Studio Code平台
- 确认已安装c/c++插件
- 在.vscode文件夹launch.json文件修改"cwd"="数据集目录地址"
- 点击F5即可运行

输出的稠密点云.ply文件在/dense_output/文件夹下，结果以运行时间命名。
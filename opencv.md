OPENCV 里的常用数据结构

cv::MAT和cv::MAT的创建方法：
    MAT A=B;拷贝构造函数
    MAT A（rows,cols,CV_8UC1,Scalar()）;构造函数
    MAT A（Size，CV_8UC1,Scalar()）;构造函数
    MAT A; A.create（rows，cols，CV_8UC1）；MAT.create成员函数
    MAT::eye（rows,cols,CV_8UC1）;单位矩阵
    MAT::zeros（rows，cols，CV_8UC1）;全零矩阵
    (MAT_<double>(rows,cols)<<1,2,3,4，...)；MAT_容器
    MAT A=MAT.clone（）；MAT.clone()成员函数
    MAT A; MAT.copyTo（A）；MAT.copyTo（）成员函数
    MAT只有copyTo（）和clone（）方法是深度拷贝，赋值或拷贝构造函数都是浅拷贝
MAT成员数据：
    MAT.rows,MAT.cols,MAT.type(),MAT.channels(),MAT.Size()
MAT像素访问：
    MAT.data,MAT.ptr<value type>(rows),MAT.begin<Vec3b>(),MAT.end<Vec3b>(),MAT.at<Vec3b>(rows,cols)
    MAT.isContinuous()
MAT通道分离、分离
    
cv::Point，cv::Point2f point；
point.x,point.y

Scalar(),4元素double类型数组。

Size，Size_<int>  Size.width,Size.height  整形的宽高。

Range 类似于python，matlab中的range
Range（start，end）表示start到end-1连续序列
Range::all（）表示所有的行或列

Rect rect;
rect.x,rect.y,rect.width,rect.height,rect.Size(),rect.area(),rect.tl(),rect.br(),rect1 & rect2,rect1 | rect2,rect+point,rect+size。
左上角横纵坐标，矩形宽高，（宽高），面积，左上角、右下角坐标，矩形交集、并集，矩形平移，伸缩

cvtColor（srcimage，dstimage，COLOR_BGR2HSV...）
COLOR_BGR2GRAY,COLOR_BGR2HSV,COLOR_BGR2YCrCb,(常用的颜色空间:GRAY,RGB,HSV,YCrCb；BGR是默认读取的彩色模式)







OPENCV不常用功能

基本图形绘制
circle；圆形
rectangle；矩形
line；线段

给图片注释文字
putText
annotation

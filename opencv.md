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
    split(MAT,MAT Vector),merge(MAT Vector,MAT)
    
点    
cv::Point，cv::Point2f point；
point.x,point.y

4元素double类型数组
Scalar()

Size类
Size，Size_<int>  Size.width,Size.height  整形的宽高。

Range 类似于python，matlab中的range
Range（start，end）表示start到end-1连续序列
Range::all（）表示所有的行或列

矩形类
Rect rect;
rect.x,rect.y,rect.width,rect.height,rect.Size(),rect.area(),rect.tl(),rect.br(),rect1 & rect2,rect1 | rect2,rect+point,rect+size。
左上角横纵坐标，矩形宽高，（宽高），面积，左上角、右下角坐标，矩形交集、并集，矩形平移，伸缩

颜色空间转换
cvtColor（srcimage，dstimage，COLOR_BGR2HSV...）
COLOR_BGR2GRAY,COLOR_BGR2HSV,COLOR_BGR2YCrCb,(常用的颜色空间:GRAY,RGB,HSV,YCrCb；BGR是默认读取的彩色模式)

MAT读取、展示、保存
imread(path,readmode)  readmode:IMREAD_UNCHANGED-1,IMREAD_GRAY 0,IMREAD_COLOR 1 OR >0,IMREAD_ANYDEPTH 2,IMREAD_ANYCOLOR 4
imshow(windowname,mat)
imwrite（path,mat）
窗口创建、消除
namedWindow(name,mode)  WINDOW_AUTOSIZE,WINDOW_NORMAL
destroyWindow(name),destroyAllWindows() 不需手动调用，程序退出时，自动销毁 窗口

OPENCV 常用的函数
waitKey（）  给定的时间内(ms)等待用户按键触发，返回按键对应的ASC码;如果用户没有按下键,则接续等待。
saturate_cast<value type>()   防数据溢出：(如value type为uchar，则data<0？0：data or data>255?255:data)

OPENCV不常用功能

基本图形绘制
circle；圆形
rectangle；矩形
line；线段

给图片注释文字
putText
annotation

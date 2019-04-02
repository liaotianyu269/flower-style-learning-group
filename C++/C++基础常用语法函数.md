<details><summary>计时函数：</summary>

getTickCount()
getTickFrequency()
如果想提高精度，QueryPerformanceCounter和QueryPerformanceFrequency可以获得低于1ms的精度。

</detailes>

类型转换：
static_cast<value type>()   一般基础类型的转换时没问题的

暂停关闭程序
system("pause")

size_t  
size_t是unsigned int  
为了增强程序的可移植性，不同系统上，定义size_t可能不一样。在32位系统中size_t是4字节的，在64位系统中，size_t是8字节的，  
这样利用该类型可以增加程序移植性。  
既然是无符号的,一般只能用在没有负数的地方，size_t一般用来表示一种计数，比如有多少东西被拷贝等。  
例如：  
sizeof操作符的结果类型是size_t，该类型保证能容纳实现所建立的最大对象的字节大小.  
它的意义大致是“适于计量内存中可容纳的数据项目个数的无符号整数类型”。所以，它在数组下标和内存管理函数之类的地方广泛使用。  

assert()

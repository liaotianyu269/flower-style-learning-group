<details><summary>基础语法：很简单的内容，可以忽略跳过。但对这部分内容需要胆大心细</summary>
  
- main()函数,include,using,cout,cin,return  
- 头文件(.hpp)  
- 命名空间  
- 常用标准库  
- 字符型，布尔型，整型，浮点型,算数运算，逻辑运算  
- 数组  
- 结构体，共用体  
- 枚举  
- if...elif...if  
- for,while,do...while...  
- switch,break,continue  
- ?:条件表达式  
- #define,typedef  
</details>

<details><summary>输入、输出和文件读取/写入</summary>

- - cin.get()之类的  
- 文件属性  
- 文件名,文件路径的操作  
- 文件读取  
- 文件写入  
...  
</details>

<details><summary>函数</summary>

- 函数的声明，定义  
- 参数  
- 返回值  
- 递归  
- 函数指针  
...
</details>

<details><summary>类</summary>
  
- 类的声明，定义，public,protected,private，成员函数，成员数据  
- 构造函数，析构函数  
- 函数重载  
- 友元函数  
- 内联函数  
- 虚函数  
- 类的继承，基类，派生类  
- 继承权限，派生类与基类的关系  
- this指针  
- 类的设计技巧  
...
</details>

<details><summary>字符串操作</summary>
  
- string类  
- 
...
</details>

<details><summary>指针，引用，const</summary>
  
- 指针*  
- 引用&  
- const  
...
</details>

<details><summary>内存管理</summary>
  
- new  
- delete  
- malloc  
...
</details>

<details><summary>模板</summary>
  
- 函数模板  
...
</details>

<details><summary>容器</summary>
  
- vector  
- pair  
...
</details>

<details><summary>异常处理</summary>
  
- exception  
...
</details>

<details><summary>数据结构</summary>
  
...
</details>

<details><summary>算法</summary>
  
...
</details>

<details><summary>其他</summary>
  
- 名称空间  
- 作用域  
- RTTI  
- 按位运算符  
- 编程思想  
...
</details>

计时函数：
getTickCount()
getTickFrequency()
如果想提高精度，QueryPerformanceCounter和QueryPerformanceFrequency可以获得低于1ms的精度。

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

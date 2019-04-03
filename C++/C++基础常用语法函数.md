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

- cin.get()之类的  
- printf  
- sprintf  
- 文件属性  
- 文件名,文件路径的操作  
  struct \_finddata_t 结构体用来存储文件信息，在<io.h>头文件中：  
  ```C++  
  struct _finddata_t{  
        unsigned attrib;            \\_A_SUBDIR 文件夹 其他选项不怎么用
        char name[_MAX_NAME];     \\文件名
        time_t time_create;        \\这些不常用
        time_t time_access;  
        time_t time_write;  
        _fsize_t size;  
         }
  ```  
  文件路径操作\_findafirst(),\_findnext(),\_findclose():  
  ```
  long _findfirst(char * path,struct _finddata_t * fileoinfo)  
  path支持通配符(*.jpg表示path下的所有.jpg文件)并将文件信息存储到fileinfo中  
  成功返回一个long型的数值，不成功返回-1  
  int _findnext(long handle,struct _finddata_t * fileinfo)  
  从句柄所指文件下一个文件开始搜索，将下一个文件信息存储到fileinfo中  
  成功返回0，不成功返回-1  
  int _findclose(long handle)  
  关闭句柄，停止搜索
  成功返回0，不成功返回-1  
  ```
  <details><summary>_finddata_t及其操作的用法</summary>  
  
  写一个遍历文件夹中.jpg文件,并将文件路径存储在.txt文件中，简单示例:  
  ```C++  
  #include<io.h>
  #include<vector>
  #include<iostream>
  #include<fstream>
  #include<string>

  using namespace std;

  void GetAllFiles(char * path, vector<string>& file)
  {
    intptr_t handle;
    _finddata_t fileinfo;
    char temppath[100];
    strcpy_s(temppath, path);
    strcat_s(temppath, "\\*");
    if ((handle = _findfirst(temppath, &fileinfo)) != -1)
    {
      do
      {
        if (strcmp(fileinfo.name, ".") != 0 && strcmp(fileinfo.name, "..") != 0)
        {
          char temp[100];
          if (fileinfo.attrib == _A_SUBDIR)
          {
            strcpy_s(temp, path);
            strcat_s(temp, "\\");
            strcat_s(temp, fileinfo.name);
            GetAllFiles(temp, file);
          }
          else
          {
            strcpy_s(temp, path);
            strcat_s(temp, "\\");
            strcat_s(temp, fileinfo.name);
            file.push_back(temp);
          }
        }
      } while (_findnext(handle, &fileinfo) == 0);
      _findclose(handle);
    }
  }
    void OutputFileName(vector<string>& file, char* filepath)
    {
      ofstream outfile(filepath);
      vector<string>::iterator it = file.begin();
      for (; it != file.end(); it++)
      {
        cout << *it << endl;
        outfile << *it << endl;
      }
      outfile.close();
    }
    void main(){
      char * RootPath = "C:\\Users\\12267\\Desktop\\Face";
      char * FilePath = "C:\\Users\\12267\\Desktop\\liaodi.txt";
      vector<string> ImagePath;
      GetAllFiles(RootPath, ImagePath);
      OutputFileName(ImagePath, FilePath);
      system("pause");
    }
  ```
  </details>
  
- 文件读取  
  <details><summary>文件读取定义、读取、文件读取关闭</summary>
  
  ```C++
  ifstream infile("path") 
  //ifstream infile;
  //infile.open("path",ios::in|ios::binary|ios::ate) //在读取时ios::ate定位到文件末尾
  infile.isopen() //打开是否成功
  while(!infile.eof()){
  infile.getline(buffer,100);//按行读取
  }
  infile.close();  
  ```
  对于如何读取有多种读取方式：  
  按行读取getline(infile,buffer);//最常用    
  getline(infile,buffer,"!");//读取一行，并以"!"作为结尾  
  </details>
- 文件写入  
  <details><summary>文件写入定义、写入、文件写入关闭</summary>
  
  ```C++
  ostream outfile("path") 
  //ostream outfile;
  //outfile.open("path",ios::out|ios::app|ios::trunc|ios::binary|ios::ate)  
  //ios::app追加写入，ios::trunc删除文件再重新创建，ios::ate清空文件  
  outfile.isopen()   //打开是否成功
  outfile<<buffer<<endl; 
  outfile.close();
  ```
  </details>
- 文件流的状态标志符  

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
  
字符串主要了解C语言字符串chars，C++字符串string。两者在操作上有区别，注意区分。  
char数组一定要初始化。。  
ep:  
char s[100]={0};//初始化为全0；
char s2[100];
memset(s2,0,sizeof(s2));//初始化全零。  
结构体也要初始化，一定要养成好习惯！！！！  
struct ss{
...
}sy;
memset(&sy,0,sizeof(sy));

- string类  
- strcmp(str1,str2) 相等返回0
- strcpy  复制字符串  
- strcat  连接字符串  
- strcnmp 比较两个字符串前n位  
## memcpy与strcpy的区别  
strcpy只能拷贝字符串，memcpy可以拷贝包括字符串以外的数据，比如结构体。strcpy遇到\0拷贝结束，这很容易造成待拷贝的函数内存溢出。  
memcpy用来在内存中复制数据，由于字符串是以 \0结尾的，所以对于在数据中包含 \0的数据只能用memcpy。  
Strncpy和memcpy很相似，只不过它在一个终止的空字符处停止。当n>strlen(s1)时，给s2不够数的空间里填充“\0”；当n<=strlen(s1)时，s2是没有结束符“\0”的。  
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

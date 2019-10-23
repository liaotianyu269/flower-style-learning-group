# Python module的概念  
  - module  
    一个.py文件即为一个module（模块）  
    分模块维护，可提高代码的维护性  
  - 包
    一个文件夹，且文件夹内需包含一个__init__.py文件，这个文件夹和__init__.py一起构成包  
    在包内可以有.py文件  
    在包内也可以有子包  
    \_\_init\_\_.py文件中默认包含了包中的所有.py文件模块和子包模块（子包整体也看成一个模块）  
  - 模块引用路径  
    包名.子包名.模块名（不带.py后缀）  
    在__init__.py中包含的模块名，可直接通过包名.模块名引用  
  ```python
      mycompany
     ├─ web
     │  ├─ __init__.py
     │  ├─ utils.py
     │  └─ www.py
     ├─ __init__.py
     ├─ abc.py
     └─ xyz.py
     ├─ utils.py
  ```
  module路径如下：  
  mycompany.web.www mycompany.abc  mycompany.xyz mycompany.utils mycompany.web.utils  
  如果mycompany的__init__.py中有这样的语句:from .web import www  or from mycompany.web import www  
  则直接引用 from mycompany import www  
# 基础语法  
    input()  输入，接收的是字符串格式    
    print("%",(,))  格式化输出  
    for 
    while  
    do...while...  
    if...elif...else...  常用的循环和判断  
    import...   
    from... import...  导入功能模块，相当于c++ include  
    # 单行注释  
    '''... ''' 多行注释  
    : 和缩进来表示代码块：相当于C++中的{}，一般一个table或4个空格的缩进表示不同层级的代码块，如下    
    ```
    if a>b:
        print(a)  
    ```
    Python对大小写敏感，写错大小写，程序会爆粗。  
    数据类型，python没有对变量数据类型的命名。整数，浮点数，字符串。其中数值型处理和C++类似，字符串的处理操作是常用的，重点的内容。   
# 基础数据结构  
    list    []类似于数组vector，可以包含不同类型的元素    
    tuple   ()类似于数组，但是tuple一旦初始化，元素不可修改，可以增加删除元素，空tuple：()，只有一个元素的tuple加逗号：(1,)  
            (1)表示数字1，不表示tuple  
    dict    {}键值对为元素的数组,如{a:1,b:2}，自如其名，就是用来查东西的，查找效率较高，dict中的键值必须是不可变对象。 
    set     set与dict类似，可以看做没有value的dict，也可看做是一个无序和无重复的元素集合。
## 元素的索引方式
- list
     与数组访问类似，带冒号是切片的访问方式  
     list[n],list[-n],list[n:m],list[:],list[::-1],list[n:],list[:n]  
     第n-1个，倒数第n个，n-1到m-1个，顺序的所有，倒叙的所有，从n-1到最后，从头到n-1  
- tuple
     与list类似
- dict
     dict索引按键值查找,比如a=dict(1:1,2:2) a[1]表示1  
- set
    与dict类似
## list，tuple,dict操作
    list() 或[]      list初始化  
    列表生成器[加for循环]   list初始化  
    list.append(),list.extend([]),list.insert(index,elem),list*num  
    list.remove(value),list.pop(index)  
    list.index()，list.count()    
    list[1:]='ython' list[0:0]='abc' list[0:3]=[] 注：分片赋值  
    list.reverse(),reversed()  
    list.sort(key,reverse=False)就地排序,sorted(list)赋值排序  
    dict() 或{}      dict初始化  
    dict.pop(key)    删除键值对并返回值  
    del dict[key]    删除键值对  
    dict.clear()     清空字典  
    dict[key]=value  增加键值对  
    dict.get(key,value=None)  返回key对应的值，没有则返回value    
    dict.update(dict1)  将dict1的键值对赋给dict  
    dict.item()      以列表形式返回k-v对  
    dict.keys()      以列表形式返回k  
    dict.values()    以列表形式返回v  
    set（[]）         set初始化必须是一个列表输入  
    set.add()         set增加元素  
    set.remove()      set删除元素  
    set1 & set2 ,set1 |set2     set的交集、并集  
    set1.difference(set2), set1.intersection(set2) 不同的元素，相同元素  
    set.clear()     清空  
    sorted(dict,key,reverse) 给字典排序  
    sorted(dict.items(),key,reverse)  
# 有序字典  
   ```python
   from collections import OrderedDict
   orderdict=OrderedDict()
   ```
# 函数  
 - 函数定义  
   使用def语句，依次写出函数名、括号、括号中的参数和冒号:  
   然后，在缩进块中编写函数体，如果什么都不做,可以用 pass  
   函数的返回值用return语句返回  
   **参数定义的顺序必须是：位置参数、可变参数、命名关键字参数和关键字参数**  
 - 函数参数    
   位置参数：有变量名，必输  
   可变参数：\*+变量名，为一个列表，存储输入的值  
   关键字参数：\*\*+变量名，为一个字典，存储键值对  
   命名关键字参数：\*,+变量名，为一个key，存储相应key的value    
 - 递归函数  
   函数内部调用自身函数。  
   思想类似数学归纳法，如果问题可以拆分为最后一步和之前的n-1复杂度的同类型问题，则可以用递归函数。  
   类似于数列递推公式，如果问题是有明确的递推规律，则可以用递归函数。  
   递归栈溢出，尾递归。待了解  
# 常用的函数
enumerate()  
isinstance(variable,type)  
hasattr(object,name)  //判断对象是否包含对应的属性,有返回true，否则返回false。  
getattr(object,name,defaultvalue)//存在就打印出来，若不存在则返回默认值若不设置默认值，则会报错    
setattr(object,name,value)//给对象属性赋值，若属性不存在，先创建属性，再赋值  
# 高级函数  
map(function,iterable) 返回一个迭代器  
reduce(function(x,y),iterable) 返回最后的计算结果,function必须是接收两个参数  
filter(function,iterable)  返回一个迭代器，根据function返回值是True或False来决定是否留下元素。  
lambda variable:表达式  lambda冒号前的是参数，函数返回值就是表达式的结果  
zip(一个或多个迭代器)  将多个对应位置的元素组成新的一组tuple，返回一个迭代器。  
zip(\*迭代器) 将迭代器最外面的[]去掉，里面的元素成为zip的迭代器进行处理。  
# 生成器、迭代器
生成器与列表生成器类似，只是用()而不是[]，用for循环访问元素，生成器、迭代器节省空间。
# 类
class.__dict__  
---
# 字符串  
不管是C++还是python，字符串、文件读写或文件路径的操作都是字符串的操作，字符串操作是共有且常用的问题，有必要专题整理总结  

---
## 字符编码方式  
python中三种编码方式 : ascii unicode utf-8  
区别：  
ascii 一个字节 只能表示英文字母数字等，不能表示其他语言字符  
unicode 两个字节或更多字节 兼容ascii 支持多语言 但是对纯英文的字符编码，空间利用率不高  
utf-8 可变长编码 如英文一字节，中文三字节 兼容ascii 支持多语言 针对不同类型字符采用不同长度空间编码  
转换方式：  
内存中采用unicode 在外部存储中采用ascii或utf-8  
内存到文件，将字符编码为ascii或utf-8存储  
文件到内存，将ascii或utf-8字符解析为unicode使用  
文本编辑器设置为utf-8 without BOM 并且在代码前注明`#-*- coding=utf-8 -*-`  则该文本采用utf-8方式进行编码  
## python的字符串
    字符串类型str，可以看做是一个含有相应字符的列表。  
    ord()，chr()     对应字符的阿斯卡码，阿斯卡码对应的字符  
    len（str）       表示字符串的字符数量  
    str.find(),str.replace(),' '.join(str),str.split(' '),str.rstrip(),str.lstrp(),str.strip(),str.strip(chars)    
    str.swapcase(),str.lower(),str.upper(),str.title()  
    str.ljust(width,char),str.rjust(width,char),str.center(width,char)  
    str.count(),str.endswith(),str.startswith()
    str.isalpha(),str.isdigit(),str.isalnum(),str.isspace(),str.islower(),str.isupper(),str.istitle()
---
## 文件读写
    with open(path,mode) as file:  
    open(filepath,mode,encoding)  encoding指定文件编码方式  
    file.readlines()  返回按行读取的迭代器  
    file.write(str)   注：写入数据类型需是字符串  
---
## 文件路径操作
- os模块，import os  
  - 文件路径的增删改查，对实际文件路径的操作
    os.getcwd()  获取当前路径  
    os.listdir()  当前目录的文件夹及文件，列表形式返回  
    os.mkdir()  创建文件路径，不能创建多级的文件路径  
    os.chdir()  改变工作目录路径  
    os.makedirs()  创建路径可以是多级的  
    os.walk()  文件夹遍历函数，列表形式返回，[当前访问的文件夹，[此文件夹下的文件夹],[此文件夹下的文件]] 
    os.rmdir()  删除路径
    os.remove()     删除文件
    os.rename(old,new)  重命名文件
  - 文件路径的操作，文件路径只作为一个字符串处理，不涉及实际文件路径的操作  
    os.path.isfile()  判断是否为文件  
    os.path.isdir()  判断是否为文件夹  
    os.path.join()   以'\\'连接字符串  
    os.path.split()  分割文件路径和文件，以列表形式返回路径和文件  
    os.path.exists()  路径是否存在  
    os.path.splitext()  返回扩展名和其余部分  
    os.path.splitdrive()  返回驱动器名和其余部分  
    os.path.dirname()  获取路径名  
    os.path.basename()  获取文件名  
- shutil模块，可以看做os模块的补充  
    shutil.copyfile(src,dst)  src源文件，dst目标文件，不存在就创建存在被覆盖  
    shutil.move(src,dst)  相当于剪切，src源文件，dst目录，如果dst下有同名的文件则报错，没有则移动成功  
    shutil.copy(src,dst)  src源文件,dst目标文件或目录,不存在就创建存在则被覆盖  
    shutil.copytree(src,dst)  将src目录下的内容复制到dst下，如果目录dst存在则报错，不存在则成功  
## 正则表达式
用来匹配字符串的强有力的武器  
# 序列化 JSON  
使用json来序列化对象，json序列化是各语言兼容的标准，速度更快  
  

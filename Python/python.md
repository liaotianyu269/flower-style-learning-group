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
    数据类型，python没有对变量数据类型的命名，但是有数据类型，整数，浮点数，字符串。其中数值型处理和C++类似，  
    字符串的处理操作是常用的，重点的内容。   
# 基础数据结构  
    list    []类似于数组vector，可以包含不同类型的元素    
    tuple   ()类似于数组，但是tuple一旦初始化就不可以修改，不能增加，删除之类的，只能访问查询，空tuple()，只有一个元素的tuple加逗号(1,)
            (1)表示数字1，不表示tuple
    dict    {}键值对为元素的数组,如{a:1,b:2}  
## 元素的索引方式
    - list
        与数组访问类似，带冒号是切片的访问方式  
        list[n],list[-n],list[n:m],list[:],list[::-1],list[n:],list[:n]  
        第n-1个，倒数第n个，n-1到m-1个，顺序的所有，倒叙的所有，从n-1到最后，从头到n-1  
    - tuple
        与list类似
    - dict
        dict索引按键值查找
---
**不管是C++还是python，字符串、文件或文件路径的操作都是共有且常用的，有必要专题整理总结**
---
# 字符编码方式
# python的字符串
    字符串类型str，可以看做是一个含有相应字符的列表。  
    ord()，chr()     对应字符的阿斯卡码，阿斯卡码对应的字符  
    len（str）        表示字符串的字符数量  
# 字符串操作

---
# 文件读写
    with open(path,mode) as file:  文件读取或写入mode='r','w','a'还有**二进制文件读取或写入mode='rb','rw'，待了解二进制文及其读写方式**  
    file.readlines()  按行读取的迭代器  
    file.write()  写入数据类型需是字符串  
---
# 文件路径操作
- os模块，import os  
  - 文件路径的增删改查，对实际文件路径的操作
    os.getcwd()  获取当前路径  
    os.listdir()  当前目录的文件夹及文件，列表形式返回  
    os.mkdir()  创建文件路径，不能创建多级的文件路径  
    os.chdir()  改变工作目录路径  
    os.rmdir()  删除路径，只能是空的文件夹，并且是一级一级的删，不能一次性多级  
    os.makedirs()  创建路径可以是多级的  
    os.removedirs()  删除多级文件夹路径，可以是多级的但是必须是空文件夹  
  - 文件的增删  
    os.remove
  - 文件路径的操作，文件路径只作为一个字符串处理，不涉及实际文件路径的操作  
    os.path.isfile()  判断是否为文件  
    os.path.isdir()  判断是否为文件夹  
    os.path.split()  分割文件路径，以列表形式返回  
    os.path.splitext()  获取扩展名  
    os.path.splitdriver()  获取驱动盘  
    os.path.dirname()  获取路径名  
    os.path.basename()  获取文件名  
  - 文件路径操作的函数  
    os.walk()  文件夹遍历函数，列表形式返回，[当前访问的文件夹，[此文件夹下的文件夹],[此文件夹下的文件]]  

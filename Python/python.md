# 基础语法  
    for 
    while  
    do...while...  
    if...elif...else...  常用的循环和判断  
    import...   
    from... import...  导入功能模块，相当于c++ include  
---
**不管是C++还是python，字符串、文件或文件路径的操作都是共有且常用的，有必要专题整理总结**
---
# 字符串操作
- 字符串
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

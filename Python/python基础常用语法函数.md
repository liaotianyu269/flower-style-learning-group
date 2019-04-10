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
    list.append(),list.extend([]),list.insert(index,elem),list.remove(value),list.pop(index),list*num  
    list.count(),list.index(),list.sort(key,reverse=False)就地排序,sorted(list)赋值排序,list.reverse(),reversed()  
    list=list('peal') list[1:]='ython' list[0:0]='abc' list[0:3]=[] 注：分片赋值  
    dict() 或{}      dict初始化  
    dict.pop(key)    删除键值对  
    dict[key]=value  增加键值对  
    dict.item()      返回k-v对  
    set（[]）         set初始化必须是一个列表输入  
    set.add()         set增加元素  
    set.remove()      set删除元素  
    set1 & set2 ,set1 |set2     set的交集、并集  
    set1.difference(set2), set1.intersection(set2) 不同的元素，相同元素  
    set.clear()     清空  
# 常用的函数
enumerate()  
isinstance(variable,type)  
map(function,iterable) 返回一个迭代器  
reduce(function(x,y),iterable) 返回最后的计算结果,function必须是接收两个参数  
lambda variable:表达式  lambda冒号前的是参数，函数返回值就是表达式的结果  
filter(function,iterable)  返回一个迭代器，根据function返回值是True或False来决定是否留下元素。  
zip(一个或多个迭代器)  将多个对应位置的元素组成新的一组tuple，返回一个迭代器。  
zip(\*迭代器) 将迭代器最外面的[]去掉，里面的元素成为zip的迭代器进行处理。  
hasattr(object,name)  //判断对象是否包含对应的属性,有返回true，否则返回false。  
getattr(object,name,defaultvalue)//获取对象属性，若存在就打印出来，若是函数则打印函数地址，若不存在则返回默认值  
                                  若不设置默认值，则会报错。  
setattr(object,name,value)//给对象属性赋值，若属性不存在，先创建属性，再赋值  
import warnings  warnings.warn('')//发出警告，但是不影响程序执行  
from tqdm import tqdm  tqdm(iterator) //带进度条输出的迭代器with tqdm(iterator) as pbar:pbar.update(n)每n个输出一次  
pbar.set_description('')  
from torchsummary input summary  summary(model,inputsize())  
os.system(shell脚本)  Python中执行shell脚本的命令，os.system调用系统shell执行接口  
argparse argparse.ArgumentParser() argparse.ArgumentParser.add_argument() argparse.ArgumentParser.parse_args()  
# 生成器、迭代器
生成器与列表生成器类似，只是用()而不是[]，用for循环访问元素，生成器、迭代器节省空间。

---
# 字符串  
不管是C++还是python，字符串、文件读写或文件路径的操作都是字符串的操作，字符串操作是共有且常用的问题，有必要专题整理总结  

---
## 字符编码方式
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
    with open(path,mode) as file:  文件读取或写入mode='r','w','a'还有**二进制文件读取或写入mode='rb','rw'，待了解二进制文及其读写方式**  
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
 **待补充**  
## 正则表达式
用来匹配字符串的强有力的武器  
**待补充**
  

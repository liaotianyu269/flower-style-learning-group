# vector
vector是一个模板容器 vector< 类型 > 标识符（最大容量，初始所有值）;  
<details><summary>vector操作</summary>
  
vector<value type>::iterator it 迭代器  
vector.begin(),vector.end()  头和尾+1迭代器  
vector.front(),vector.back()  第一个和最后一个元素  
vector.at<value type>(d1,d2,...) or vector[index]  访问元素  
vector.data  第一个元素的指针  
vector.push_back(),vector.insert(position,elem) 添加元素    
vector.pop_back(),vector.erase(n or [])  删元素  
vector.swap(vector)  交换   
vector.clear()  清空  
vector.size(),vector.max_size(),vecotr.capacity(),vector.resize(),vector.reserve()  
vector.empty(),vector.shrink_to_fit()  
vector.assign(n,t) or vector.assign(const_iterator first,const_iterator last)  
</details>
  
# pair
pair是一个模板容器 pair<value type,value type> p(初始化1，初始化2)或pair=make_pair(初始化1，初始化2)，如下  
```
vector<pair<int,int>>VP;  
VP.push_back(make_pair<int,int>(10,50));  
```
pair.first, pair,second第一个参数，第二个参数  
pair 比较操作数，可以用== != < <= > >=比较大小，比较规则是先以first的大小作为标准，只有当first相等时才取判别second的大小  
# map&multimap  
map是key不重复的以key-value对为元素的有序容器，key,与value是一对一的关系,自动根据key排序  
<details><summary>map操作</summary>
  
```C++
  map<value type,value type> m;  //创建三种方式,insert，数组形式
  m.insert(pair<valuetype,valuetype>(a,b));
  m.insert(map<valuetype,valuetype>::value_type(a,b));//insert重复键值，value不被覆盖,返回插入位置迭代器和成功标识
  m.[key]=value;//赋值重复键值，value被覆盖
  map.size(),map.begin(),map.end(),map.empty(),map.rend(),map.rbegin()
  //元素个数，第一个迭代器，尾迭代器+1，是否为空，最后一个迭代器，第一个迭代器-1.
  map遍历,可以用数组形式或迭代器。
  //map<valuetype,valuetype>::iterator 或reverse_iterator，注意正向和反向迭代器区别。
  //反向迭代器从指定位置按-1的规则遍历，寄reverse_iterator++,相当于从a的位置到a-1的位置。
  map.find(),map.lower_bound(),map.upper_bound(),map.equal_range().
  //返回相应值的迭代器，未找到返回end().lower>=,upper>，equal_range返回一对迭代器pair<lower_bound,upper_bound>.
  map.erase(迭代器或key),map.clear()//erase可以删一个或连续几个,clear清空
  map.swap(map)//两个map元素全部交换
```
</details>
multimap是key可重复的以key-value对为元素的有序容器。一个key,可以有多个value，自动根据key排序  
<details><summary>multimap操作</summary>
    
```C++
  multimap<value type,value type> m;  //创建，只能用insert，不能数组形式
  m.insert(pair<valuetype,valuetype>(a,b));//insert重复键值，会被重复添加,返回插入位置迭代器和成功标识
  m.insert(multimap<valuetype,valuetype>::value_type(a,b);
  multimap.size(),multimap.begin(),multimap.end(),multimap.empty(),multimap.rend(),multimap.rbegin()
  //元素个数，第一个迭代器，尾迭代器+1，是否为空，最后一个迭代器，第一个迭代器-1.
  map遍历,只能用迭代器。
  //multimap<valuetype,valuetype>::iterator 或reverse_iterator，注意正向和反向迭代器区别。
  //反向迭代器从指定位置按-1的规则遍历，寄reverse_iterator++,相当于从a的位置到a-1的位置。
  multimap.find(),multimap.lower_bound(),multimap.upper_bound(),multimap.equal_range().
  //返回第一个相应值的迭代器，未找到返回end().lower>=,upper>，equal_range返回一对迭代器pair<lower_bound,upper_bound>.
  map.erase(迭代器或key),map.clear()//erase可以删一个或连续几个,clear清空
  map.swap(map)//两个map元素全部交换
  multi.count()//计数
```
</details>  

# set&multiset  
set是一个自动排序的无重复元素的容器，set中的值不能直接被改变。  
multiset是一个自动排序的可重复元素的容器。  
如果删除元素a,那么在定义的比较关系下和a相等的所有元素都会被删除  
<details><summary>set&multiset操作</summary>
  
set\multiset.count( a )：set能返回０或者１，multiset是有多少个返回多少个．  
Set和multiset都是引用<set>头文件,复杂度都是logn  
set.insert(),set.erase(),set.find(elem),set.begin(),set.end(),set.size(),set.max_size().set.empty(),set.clear()，set.count()  
set.lower_bound(),set.upper_bound()  同vector的相应功能  
insert(key_value); 将key_value插入到set中  
返回值是pair<set<int>::iterator,bool>，bool标志着插入是否成功，而iterator代表插入的位置，  
若key_value已经在set中，则iterator表示的key_value在set中的位置。  
inset(first,second);将定位器first到second之间的元素插入到set中，返回值是void.  
lower_bound(key_value) ，返回第一个大于等于key_value的定位器  
upper_bound(key_value)，返回第一个大于key_value的定位器  
</details>

# queue
# priority_queue  
priority_queue<Type, Container, Functional>，其中Type 为数据类型，Container为保存数据的容器，Functional 为元素比较方式。  
Container必须是用数组实现的容器，比如vector,deque等等，但不能用 list。STL里面默认用的是vector。 

# deque 
  deque(双端队列)是double-ended queue的一个不规则缩写，deque是具有动态大小的序列容器，可以在两端（前端或后端）扩展或收缩。 
  双端队列，支持快速访问。在头尾位置插入/删除速度很快。 
  deque在接口上和vector很相似，在许多地方可以直接替换  
  deque可以随机存取元素，支持索引值直接存取，使用[]或者是at()方法  
  deque的头部和尾部添加和移除元素都非常快速，但是在中部插入元素或移除元素比较费时。  
  deque的构造 和 vector基本相同  
  ```
  deque<int>de;
  ```
  方法|含义  
  ------|---------  
  deque|构造函数   
  push_back|在当前的最后一个元素之后，在deque容器的末尾添加一个新元素  
  push_front|在deque容器的开始位置插入一个新的元素，位于当前的第一个元素之前  
  pop_back|删除deque容器中的最后一个元素，有效地将容器大小减少一个  
  pop_front|删除deque容器的第一个元素，有效地减小其大小  
  emplace_front|在deque的开头插入一个新的元素，就在其当前的第一个元素之前  
  emplace_back|在deque的末尾插入一个新的元素，紧跟在当前的最后一个元素之后  
  deque.at[index]|返回索引index所指的数据，如果越界，会跑出out_of_range   
  deque[index]|返回index所指的数据，越界的话，不会抛出异常  
  deque.front()|返回第一个元素  
  deque.back()|返回最后一个元素  
  deque.begin()|返回容器中第一个元素的迭代器  
  deque.end()|返回容器中最后一个元素之后的迭代器  
  deque.rbegin()|返回容器中倒数第一个元素的迭代器 
  deque.rend()|返回容器中倒数最后一个元素之后的迭代器  
  deque(beg,end)|构造函数将区间[beg,end)区间的元素拷贝给本身  
  deque(n,ele)|构造函数将n个ele拷贝给本身  
  deque(const deque &deq)|拷贝构造函数  
  deque.assign(beg,end)|deque的赋值   
  deque.assign(n,ele)|deque的赋值  
  deque& operator=(const deque &deq)|deque的赋值 
  deque.swap(deq)|将vec与本身的元素互换  
  deque.insert(pos,elem)|在pos位置插入一个elem元素的拷贝，返回新数据的位置  
  deque.insert(pos,n,elem)|在pos位置插入n个elem数据，无返回值  
  deque.insert(pos,beg,end)|在pos位置插入[beg,end)区间的数据，无返回值  
  deque.clear()|移除容器的所有数据  
  deque.erase(beg,end)|删除[beg,end)区间的数据，返回下一个数据的位置  
  deque.erase(pos)|删除pos位置的数据，返回下一个数据的位置  
# stack  
stack对象的默认构造  
stack 是一种容器适配器，用于在LIFO（后进先出）的操作，其中元素仅从容器的一端插入和提取。  
```
//stack采用模板类实现， stack对象的默认构造形式： stack <T> stkT;  如：
stack <int> stkInt;            //一个存放int的stack容器。
stack <float> stkFloat;     //一个存放float的stack容器。
stack <string> stkString;     //一个存放string的stack容器。             
//尖括号内还可以设置指针类型或自定义类型。
```
stack的push与pop操作  
```  
stack.push(elem);   //往栈头添加元素
stack.pop();   //从栈头移除第一个元素

```
stack的数据存取  
``` 
stack.top();      //返回最后一个压入栈元素
``` 
stack的大小  
```
stack.empty();   //判断堆栈是否为空
stack.size();        //返回堆栈的大小
```
# list  
list是实现的双向链表  
```  
//1.定义和初始化  
    list<int> lst1;          //创建空list  
    list<int> lst2(3);       //创建含有三个元素的list  
    list<int> lst3(3,2); //创建含有三个元素为2的list  
    list<int> lst4(lst2);    //使用lst2初始化lst4  
    list<int> lst5(lst2.begin(),lst2.end());  //同lst4  
 
    //2.常用操作方法  
    lst1.assign(lst2.begin(),lst2.end());  //分配值,3个值为0的元素  
    lst1.push_back(10);                    //末尾添加值  
    lst1.pop_back();                   //删除末尾值  
    lst1.begin();                      //返回首值的迭代器  
    lst1.end();                            //返回尾值的迭代器  
    lst1.clear();                      //清空值  
    bool isEmpty1 = lst1.empty();          //判断为空  
    lst1.erase(lst1.begin(),lst1.end());                        //删除元素  
    lst1.front();                      //返回第一个元素的引用  
    lst1.back();                       //返回最后一个元素的引用  
    lst1.insert(lst1.begin(),3,2);         //从指定位置插入个3个值为2的元素  
    lst1.rbegin();                         //返回第一个元素的前向指针  
    lst1.remove(2);                        //相同的元素全部删除  
    lst1.reverse();                        //反转  
    lst1.size();                       //含有元素个数  
    lst1.sort();                       //排序  
    lst1.unique();                         //删除相邻重复元素  
 
    //3.遍历  
    //迭代器法  
    for(list<int>::const_iterator iter = lst1.begin();iter != lst1.end();iter++)  
    {  
       cout<<*iter;  
    }  
```  
# forward_list  
forward_list容器以单链表的形式存储元素。forward_list的模板定义在头文件forword_list中。forward_list和list最主要的区别是：它不能反向遍历元素；只能从头到尾遍历。  
forward_list 的单向链接性也意味着它会有一些其他的特性：  
无法使用反向迭代器。只能从它得到const或non-const前向迭代器，这些迭代器都不能解引用，只能自增；  
没有可以返回最后一个元素引用的成员函数back();只有成员函数front();  
因为只能通过自增前面元素的迭代器来到达序列的终点，所以push_back()、pop_back()、emplace_back()也无法使用。  

forward_list 的操作比 list 容器还要快，而且占用的内存更少，尽管它在使用上有很多限制，但仅这一点也足以让我们满意了。  

forward_list 容器的构造函数的使用方式和 list 容器相同。forward_list 的迭代器都是前向迭代器。它没有成员函数 size()，因此不能用一个前向迭代器减去另一个前向迭代器，但是可以通过使用定义在头文件 iterator 中的 distance() 函数来得到元素的个数。例如：  
```
std::forward_list<std::string> my_words {"three", "six", "eight"};  
auto count = std::distance(std::begin(my_words),std::end(my_words));  
// Result is 3  
```  
distance() 的第一个参数是一个开始迭代器，第二个参数是一个结束迭代器，它们指定了元素范围。当需要将前向迭代器移动多个位置时，advance() 就派上了用场。例如：  
```
std::forward_list<int> data {10, 21, 43, 87, 175, 351};  
auto iter = std::begin(data);  
size_t n {3};  
std::advance(iter, n);  
std::cout << "The " << n+1 << "th element is n << *iter << std::endl;  
// Outputs 87  
```  


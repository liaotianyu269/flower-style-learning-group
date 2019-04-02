# vector
vector是一个模板容器 vector< 类型 > 标识符（最大容量，初始所有值）;  
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
# pair
pair是一个模板容器 pair<value type,value type> p(初始化1，初始化2)或pair=make_pair(初始化1，初始化2)，如下  
```
vector<pair<int,int>>VP;  
VP.push_back(make_pair<int,int>(10,50));  
```
pair.first, pair,second第一个参数，第二个参数  
pair 比较操作数，可以用== != < <= > >=比较大小，比较规则是先以first的大小作为标准，只有当first相等时才取判别second的大小  
# map&multiimap
map和multimap。在存储数据时，会根据pair<>的first成员进行排序。map的key,与value是一对一的关系，multimap,一个key,可以有多个value.
# set&multiset
set是一个自动排序的无重复元素的容器，set中的值不能直接被改变。  
multiset是一个自动排序的可重复元素的容器。  
如果删除元素a,那么在定义的比较关系下和a相等的所有元素都会被删除  
set\multiset.count( a )：set能返回０或者１，multiset是有多少个返回多少个．  
Set和multiset都是引用<set>头文件,复杂度都是logn  
set.insert(),set.erase(),set.find(elem),set.begin(),set.end(),set.size(),set.max_size().set.empty(),set.clear()，set.count()
set.lower_bound(),set.upper_bound()  同vector的相应功能  
find(x)是返回的是x的值，如果x没有在set中则会输出end()  
insert(key_value); 将key_value插入到set中  
返回值是pair<set<int>::iterator,bool>，bool标志着插入是否成功，而iterator代表插入的位置，  
若key_value已经在set中，则iterator表示的key_value在set中的位置。  
inset(first,second);将定位器first到second之间的元素插入到set中，返回值是void.  
lower_bound(key_value) ，返回第一个大于等于key_value的定位器  
upper_bound(key_value)，返回第一个大于key_value的定位器  
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
  
# stack
# list
# forward_list
# queue
# priority_queue

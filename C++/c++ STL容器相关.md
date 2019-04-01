# vector
vector是一个模板容器 vector<value type,n> v(初始化序列);  
vector<value type>::iterator it 迭代器  
vector.begin(),vector.end()  头和尾+1迭代器  
vector.front(),vector.back()  第一个和最后一个元素  
vector.at<value type>(d1,d2,...)  访问元素  
vector.data  第一个元素的指针  
vector.push_back(),vector.insert(position,elem) 添加元素    
vector.pop_back(),vector.erase(n or [])  删元素  
vector.swap(vector)  交换   
vector.clear()  清空  
vector.size(),vector.max_size(),vecotr.capacity(),vector.resize(),vector.reserve()  
vector.empty(),vector.shrink_to_fit()  

# pair
pair是一个模板容器 pair<value type,value type> p(初始化1，初始化2)  
pair=make_pair(初始化1，初始化2) pair需要是定义的相应类型的pair，如下  
pair 写法：vector<pair<int,int>>VP;  VP.push_back(make_pair<int,int>(10,50));
pair.first, pair,second第一个参数，第二个参数  


# List

# map&multiimap

map和multimap。在存储数据时，会根据pair<>的first成员进行排序。map的key,与value是一对一的关系，multimap,一个key,可以有多个value.

# set&multiset

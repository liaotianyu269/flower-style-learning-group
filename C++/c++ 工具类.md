# 时间相关函数 

string类型转换成时间类型（time_t) 

```
time_t base_tool：：StringToDatetime(char *str)  
{  
	tm tm_;  
	int year, month, day, hour, minute,second;  
	sscanf(str,"%d-%d-%d %d:%d:%d", &year, &month, &day, &hour, &minute, &second);  
	tm_.tm_year  = year-1900;  
	tm_.tm_mon   = month-1;  
	tm_.tm_mday  = day;  
	tm_.tm_hour  = hour;  
	tm_.tm_min   = minute;  
	tm_.tm_sec   = second;  
	tm_.tm_isdst = 0;  

	time_t t_ = mktime(&tm_); //已经减了8个时区  
	return t_; //秒时间  
}  

```
# 添加(\)，防止一个(\)被转义，利用函数，转换成(\\) 
``` 
int  string_replase(string &s1, const string &s2, const string &s3)
{ 
	string::size_type pos = 0; 
	string::size_type a = s2.size(); 
	string::size_type b = s3.size(); 
	while ((pos = s1.find(s2, pos)) != string::npos)  
	{ 
		s1.replace(pos, a, s3); 
		pos += b; 
	} 
	return 0; 
} 
``` 
```
代码调eg: 
string_replase(*str, "\\", "\\\\");
```

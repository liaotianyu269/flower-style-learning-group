# 指针很重要，虽然指针很烦，但是很有用，不要逃避
## 指针类型和指针遍历长度的关系  
 今天在看opencv的时候了解到一点，关于访问MAT矩阵的元素时，指针的运用：  
 就是在获取MAT首地址或某行的首地址后，再转换指针的类型，可以改变指针访问元素的方式。  
 例如(uchar*) pointer ，pointer++表示，pointer向后移动了一个uchar的长度  
 如果(float*) pointer , pointer++表示，pointer向后移动了一个float的长度  
 

##指针相关
指针的长度为4
Int *p;
Double *q;
Sizeof(p)=sizeof(q)=4;

同时使用 new和delete
Int *s=new int;
Delete s;
Int *p=new int[10];
Delete[] p;
#指针的指向的值与地址：
nt s[7]={0};
	
int *p=s;
*p=s=0//值相等
&s的地址与p值相等，p表示指向s的地址
&p表示指针p本身的地址。
都可以用cout<<打印出来。
如果是char 类型的
Char s[7]={0};
Memcpy_s(s,sizeof(s),"1",1);
Char *p=s;
Cout<<&S<<endl//打印的是s的地址
Cout<<&p<<endl//打印的是指针p的地址
Cout<<p<<endl//此时cout是把p指向的对象的地址转换了。
Printf("%p\n",p);打印的是p指向的地址



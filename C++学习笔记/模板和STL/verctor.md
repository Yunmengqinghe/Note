## 一、基本概念
1. 功能：vector数据结构与数组非常相似
2. vector与普通数组区别：数组是静态空间，vector可以动态扩展
3. 动态扩展：
	+ 寻找更大内存空间，将原数组拷贝到新空间，释放原来空间
	+ vector容器的迭代器支持随机访问
![[Pasted image 20230914092014.png]]
		
## 二、初始化和赋值
### 容器初始化
函数原型
```cpp
//默认构造
vector<T> v;

//左闭右开区间，将区间内的元素赋值给vector
vector(v.begin(), v.end()); 

//将n个elem拷贝给它
vector(n, elem); 

//拷贝构造
vector(const vector& vec); //拷贝构造
```

### 赋值操作
1. 函数原型
```cpp
vector& operator=(const vector &vec); //重载等号操作符 

assign(beg, end); //将[beg, end)区间中的数据拷贝赋值给本身。 

assign(n, elem); //将n个elem拷贝赋值给本身。
```
2. 常用`=`

## 三、基本操作
### 容量和大小
函数原型
```cpp
//判断容器是否为空 
empty(); 

//容器的容量 
capacity(); 

//返回容器中元素的个数 
size(); 

//重新指定容器的长度为num，若容器变长，则以默认值填充新位置
//如果容器变短，则末尾超出容器长度的元素被删除。 
resize(int num); 

//重新指定容器的长度为num，若容器变长，则以elem值填充新位置
//如果容器变短，则末尾超出容器长度的元素被删除
resize(int num, elem);  
```

### 插入和删除
函数原型
```cpp
//尾插
push_back(ele);

//尾删
pop_back();

//在pos处插入元素
insert(const_iterator pos, ele);

//指向pos插入count个元素ele
insert(const_iterator pos, int count, ele);

//删除指向的元素
erase(const_iterator pos);

//删除从strat到end的元素
erase(const_iterator start, const_iterator end);

//清空
clear();
```

### 数据存取
函数原型
```cpp
//返回索引idx所指的数据
at(int idx);

//返回索引idx所指的数据
operator[];

//返回第一个元素
front();

//返回最后一个元素
back();
```

### 元素交换
1. 原型
```cpp
//实现两个vector元素互换
swap(vec);
```

2. 作用
使用swap可以收缩内存空间
```cpp
vector<int>(v).swap(v);

//先拷贝构造v创建一个匿名对象
//再swap交换v的指向，让v的内存空间缩小
//系统会自动回收匿名对象
```
![[1694842599581.png]]

### 预留元素
1. 功能：减少vector在动态扩展容量时的扩展次数
2. 函数原型
```cpp
//容量预留len个元素，预留位置不可初始化，元素无法访问
reserve(int len);
```
## 一、概念
1. 功能：双端数组，可以对头段进行插入删除操作
2. deque和vector的区别:
	+ vector对于头部的插入删除效率低，数据量越大，效率越低
	+ deque相对而言，对头部的插入删除速度比vector快
	+ vector访问元素时的速度比deque快，这与二者实现有关
![[Deque.png]]

## 二、基本操作
### 构造函数
1. 原型
```cpp
//默认构造形式
deque<T> deqT;  

//构造函数将[beg, end)区间中的元素赋值给变量
deque<T> deqT(begin(), end()); 

//构造函数将n个elem拷贝给本身
deque<T> deqT(n, elem); 

//拷贝构造函数
deque<T> deqT(const deque &deq); 
```

### 赋值操作
1. 原型
```cpp
//运算符重载
deque& operator=(const deque &deq);

//将[beg, end)区间中的元素赋值给元素
assgin(begin(), end());

//将n个elem赋值给元素
assgin(n, elem);
```

### 大小操作
1. 原型
```cpp
//判空
deque.empty();

//返回个数
deque.size();

//重新指定容器的长度为num，若容器变长，则以默认值填充新位置
//如果容器变短，则末尾超出容器长度的元素被删除
deque.resize(num);

//重新指定容器的长度为num，若容器变长，则以elem填充新位置
//如果容器变短，则末尾超出容器长度的元素被删除
deque.resize(num, elem);
```

### 插入删除
1. 原型
```cpp
//1.两端插入操作
//尾插
push_back(elem);

//头插
push_front(elem);

//删除容器最后一个数据
pop_back();

//删除容器第一个数据
pop_front();

//2.指定指定操作
//在pos位置插入一个elem元素的拷贝，返回新数据的位置
insert(pos, elem);

//在pos位置插入n个elem数据，无返回值
insert(pos,n,elem);

//在pos位置插入[beg,end)区间的数据，无返回值
insert(pos,beg,end);

//清空容器的所有数据
clear();

//删除[beg,end)区间的数据，返回下一个数据的位置
erase(beg,end);

//删除pos位置的数据，返回下一个数据的位置
erase(pos);
```

### 数据存取
1.原型
```cpp
//返回索引index所指的数据
at(int index);

//返回缩影idx所指的数据
operator[];

//返回容器中第一个数据元素
front();

//返回最后一个数据元素
back();
```

### 排序
1. 算法：`sort(iterator beg, iterator end) //对beg和end区间元素进行排序`
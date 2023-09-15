## 一、基本概念
1. 功能：vector数据结构与数组非常相似
2. vector与普通数组区别：数组是静态空间，vector可以动态扩展
3. 动态扩展：
	+ 寻找更大内存空间，将原数组拷贝到新空间，释放原来空间
	+ vector容器的迭代器支持随机访问
![[Pasted image 20230914092014.png]]
		
## 二、初始化和赋值
### 容器初始化
1. 函数原型
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
2. 多用`=`
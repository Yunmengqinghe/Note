## STL基本概念
+ STL分为：容器、算法、迭代器
+ 容器和算法之间通过迭代器进行无缝连接

## STL六大组件
1. 基本组件：容器、算法、迭代器、仿函数、适配器(配接器)、空间适配器
	+ 容器：各种数据结构，如vector、list、deque、set、map等，用来存放数据。 
	+ 算法：各种常用的算法，如sort、find、copy、for_each等 
	+ 迭代器：扮演了容器与算法之间的胶合剂 
	+ 仿函数：行为类似函数，可作为算法的某种策略
	+ 适配器：一种用来修饰容器或者仿函数或迭代器接口的东西
	+ 空间配置器：负责空间的配置与管理

## STL中容器、算法、迭代器
### 容器
1. STL容器就是将运用最广泛的一些数据结构实现出来 
2. 常用的数据结构：数组,、链表、树、栈、队列、集合、映射表等 
3. 这些容器分为序列式容器和关联式容器两种：
	+ 序列式容器:强调值的排序，序列式容器中的每个元素均有固定的位置
	+ 关联式容器:二叉树结构，各元素之间没有严格的物理上的顺序关系

### 算法
1. 算法分为:质变算法和非质变算法
	+ 质变算法：是指运算过程中会更改区间内的元素的内容。例如拷贝，替换，删除等等 
	+ 非质变算法：是指运算过程中不会更改区间内的元素内容，例如查找、计数、遍历、寻找极值等等

### 迭代器
1. 迭代器：容器和算法之间粘合剂 
2. 提供一种方法，使之能够依序寻访某个容器所含的各个元素，而又无需暴露该容器的内部表示方 式。 
3. 每个容器都有自己专属的迭代器(迭代器使用非常类似于指针，初学阶段我们可以先理解迭代器为指针)

|种类|功能|支持运算|
|---|---|---|
|输入迭代器|对数据的只读访问|只读，支持++、\==、!=|
|输出迭代器|对数据的只写访问|只写，支持++|
|前向迭代器|读写操作，并能向前推进迭代器|读写，支持++、\==、!=|
|双向迭代器|读写操作，并能向前和向后操作|读写，支持++、--|
|随机访问迭代器|读写操作，可以以跳跃的方式访问任意数据|读写，支持++、--、[n]、-n、<、<=、>、>=|

4. 总结：常用的容器中迭代器种类为双向迭代器，和随机访问迭代器

## 迭代器初识
### vector存放内置数据类型
1. 容器：`vector`
2. 算法：`for_each`
3. 迭代器：`vector<int>::iterator`

```cpp
#include <vector>
#include <algorithm>

void MyPrint(int val) 
{ 
cout << val << endl; 
} 

int main() 
{ 
	//创建vector容器对象，并且通过模板参数指定容器中存放的数据的类型 
	vector v; 
	
	//向容器中放数据 
	v.push_back(10); 
	v.push_back(20); 
	v.push_back(30);
	v.push_back(40);
	
	//每一个容器都有自己的迭代器，迭代器是用来遍历容器中的元素 
	//v.begin()返回迭代器，这个迭代器指向容器中第一个数据 
	//v.end()返回迭代器，这个迭代器指向容器元素的最后一个元素的下一个位置 
	//vector::iterator 拿到vector这种容器的迭代器类型 
	vector::iterator pBegin = v.begin(); 
	vector::iterator pEnd = v.end(); 
	
	//第一种遍历方式： 
	while (pBegin != pEnd) 
	{
		cout << *pBegin << endl; 
		pBegin++; 
	} 
	
	//第二种遍历方式： 
	for (vector::iterator it = v.begin(); it != v.end(); it++) 
	{ 
		cout << *it << endl; 
	} 
	cout << endl;

	//第三章遍历方式，利用STL提供遍历算法
	for_each(v.begin(), v.end(), myPrint);
}
```

### vector存放自定义数据类型
1. 存类型
```cpp
#include <vector>
#include <algorithm>
class Person
{
public:
	Person(string name, int age)
	{
		this->name = name;
		this->age = age;
	}
	string name;
	int age;
}

int main()
{
	vector<Person> v;

	Person p1("cxk", 10);
	Person p2("abc", 11);

	v.push_back(p1);
	v.push_pack(p2);

	for(vector<Person>::iterator it = v.begin(); it != v.end; it++)
	{
		//解引用之后是个Person的数据类型(看<>内)
		cout << (*it).name << endl;

		//it是指向v的一个指针，类型为Person*
		cout << it->age <<endl;
	}
	
	return 0;
}
```

2. 存指针
```cpp
int main()
{
	vector<Person*> v;

	Person p1("cxk", 10);
	Person p2("abc", 11);

	v.push_back(&p1);
	v.push_pack(&p2);

	for(vector<Person*>::iterator it = v.begin(); it != v.end; it++)
	{
		cout << (*it)->name << endl;
	}
	
	return 0;
}
```

### vector容器嵌套容器
```cpp
//容器嵌套容器
int main()
{
	vector<vector<int>> v;

	//创建小容器
	vector<int> v1;
	vector<int> v2;

	//给小容器赋值
	for(int i = 0; i < 2; i++)
	{
		v1.push_back(i);
		v2.push_back(i + 1);
	}
	
	//给大容器赋值
	v.push_back(v1);
	v.push_back(v2);

	//通过大容器，把所有的数据输出
	for(vector<vector<int>>::iterator it = v.begin(); it != v.end(); it++)
	{
		for(vector<int>::iterator vit = (*it).begin(); vit != *(it).end(); vit++)
		{
			cout << *vit << endl;
		}
		cout << endl;
	}

}
```
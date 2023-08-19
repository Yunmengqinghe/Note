## 成员变量和成员函数分开储存
+ 在Cpp中，类内的成员变量和成员函数分开储存，只有非静态成员变量才属于类的对象上
```Cpp
class Person {
public:
	//非静态成员变量占对象空间
	int _a;
	
	//静态成员变量不占对象空间
	static int _b;
	
	//函数也不占对象空间，所有函数共享一个函数实例
	void func()
	{
		
	}
};
```

## this指针概念
1. 引入：每一个非静态成员函数只会诞生一份函数实例，也就是说多个同类型的对象会共用一块代码，那么这块代码如何区分是哪个对象调用自己呢
2. 解决：**this指针指向被调用的成员函数所属的对象**
3. this指针是隐含每一个非静态成员函数内的一种指针，this不需要定义
4. 实质：this指针无法修改指向，实质为`Person *const this;`，是指针常量
5. 用途：
	+ 当形参和成员变量同名时，可以用this指针来区分
	+ 在类的非静态成员函数中返回对象本身，可使用`return *this;`
```Cpp
class Person
{
public:
	Person& Age_add(Person& p)
	{
		this->age += p.age;
		//this是指向p2的指针，*this指向的是p2的本体
		return *this;
	}
	//如果是Person Age_add(Person& p)的形式，那么返回的相当于是一个新的对象，并且使用了拷贝构造函数

	int age;
};

int main()
{
	Person p1(10);
	Person p2(10);

	//链式编程思想
	p1.Age_add(p2).Age_add(p2);
}
```

## 空指针访问成员函数
+ Cpp中空指针也可以调用成员函数，但是也要注意有没有用到this指针
+ 如果用到了this指针，要加以判断保证代码的健壮性
```Cpp
class Person
{
public:
	void ShowAge()
	{
		//指针检查
		if(this == NULL)
		{
			returm;
		}
		//age相当于this->age，如果指针为空则会报错
		cout << "age = " << age << endl;
	}
	int age;
};

int main()
{
	Person* p = NULL;
	p->ShowAge();
	return 0;
}
```

## const修饰成员函数

1. 常函数：
	+ 成员函数后加`const`后我们称这个函数为常函数
	+ 常函数内不可以修改成员属性
	+ 成员属性声明加关键词`mutable`后，在常函数中依然可以修改
```Cpp
class Person
{
public:
	//在成员函数后加const，修饰的是this的指向的值，指针的值是不能修改的
	void ChangeAge() const
	{
		//会报错，此时的this指针相当于const Person *const this;
		//既不能修改指针所指方向，也不能修改指针所指数值
		this -> age = 100;
		
		//值能修改
		this -> hight = 100;
	}
	
	int age;

	//加特殊的声明能使其值在常函数中也能修改
	mutable int hight;
};
```

2. 常对象
	+ 声明对象前加`const`称改对象为常对象
	+ 常对象只能调用常函数
```Cpp
int main()
{
	//在对象前加const，变为常对象
	const Person p;
	
	//只有加了mutabale的值在常对象中能修改
	p.hight = 10;
}
```
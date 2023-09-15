## 一、基本概念
### string和char\*区别
1. char\*是一个指针
2. string是一个封装了char\*的类，是一个char\*的容器

## 二、string构造函数
1. 函数原型
+ `string()`
+ `string(const char* s)`
+ `string(const string& str)`
+ `string(int n,char c) //n个字符c进行构造`

## 三、string赋值操作
1. 功能：给string字符串进行赋值
2. 函数原型
```cpp
string& operator=(const char* s);
// 将C风格的字符串赋值给当前字符串

string& operator=(const string& s);
// 将字符串s赋值给当前字符串

string& operator=(char c);
// 将字符赋值给当前字符串

string& assign(const char* s);
// 将字符串s赋值给当前字符串

string& assign(const char* s, int n);
// 将字符串s的前n个字符赋值给当前字符串

string& assign(const string& s);
// 将字符串s赋值给当前字符串

string& assign(int n, char c);
// 使用n个字符c赋值给当前字符串
```

## 四、string拼接
1. 函数原型
```cpp
string& operator+=(const char* str); //重载+=操作符 

string& operator+=(const char c); //重载+=操作符 

string& operator+=(const string& str); //重载+=操作符 

string& append(const char *s); //把字符串s连接到当前字符串结尾 

string& append(const char *s, int n); //把字符串s的前n个字符连接到当前字符串结尾 

string& append(const string &s); //同operator+=(const string& str) 

string& append(const string &s, int pos, int n); //字符串s中从pos开始的n个字符连接到字符串结尾
```

## 五、string查找与替换
1. 原型
```cpp
int find(const string& str, int pos = 0) const;
// 在当前字符串中从位置pos开始查找字符串str第一次出现的位置

int find(const char* s, int pos = 0) const;
// 在当前字符串中从位置pos开始查找C风格字符串s第一次出现的位置

int find(const char* s, int pos, int n) const;
// 在当前字符串中从位置pos开始查找C风格字符串s的前n个字符第一次出现的位置

int find(const char c, int pos = 0) const;
// 在当前字符串中从位置pos开始查找字符c第一次出现的位置

int rfind(const string& str, int pos = npos) const;
// 在当前字符串中从位置pos开始逆向查找字符串str最后一次出现的位置

int rfind(const char* s, int pos = npos) const;
// 在当前字符串中从位置pos开始逆向查找C风格字符串s最后一次出现的位置

int rfind(const char* s, int pos, int n) const;
// 在当前字符串中从位置pos开始逆向查找C风格字符串s的前n个字符最后一次出现的位置

int rfind(const char c, int pos = 0) const;
// 在当前字符串中从位置pos开始逆向查找字符c最后一次出现的位置

string& replace(int pos, int n, const string& str);
// 将当前字符串中从位置pos开始的n个字符替换为字符串str

string& replace(int pos, int n, const char* s);
// 将当前字符串中从位置pos开始的n个字符替换为C风格字符串s
```

2. 总结
	+ find查找是从左往后，rfind从右往左 
	+ find找到字符串后返回查找的第一个字符位置，找不到返回-1
	+ replace在替换时，要指定从哪个位置起，多少个字符，替换成什么样的字符串

## 六、string的字符串比较
1. 比较结果
	+ `=`返回 0
	+ `>`返回 1
	+ `<`返回 -1
2. 函数原型
```cpp
int compare(const string& s) const; //与字符串s比较
int compare(const string& s) const; //与字符串s比较
```

## 七、string类型字符存取
1. 访问方式
	+ 通过`str[i]`访问单个字符
	+ 通过`str.at(i)`方式访问单个字符

## 八、string插入和删除
1. 函数原型
```cpp
string& insert(int pos, const char* s);
// 在当前字符串中的位置pos处插入C风格字符串s

string& insert(int pos, const string& str);
// 在当前字符串中的位置pos处插入字符串str

string& insert(int pos, int n, char c);
// 在当前字符串中的位置pos处插入n个字符c

string& erase(int pos, int n = npos);
// 从当前字符串中的位置pos开始删除n个字符，默认删除到字符串末尾
```

2. 插入和删除的起始下标都是从0开始

## 九、字串获取
1. 函数原型
```cpp
string substr(int pos = 0, int n = npos) const;
//返回由pos开始的n个字符组成的字符串
```


## 一、基本概念
1. stack是一种先进后出的数据结构

## 二、常用函数
```cpp
//默认构造函数
//创建一个空的栈对象
stack<T> stk;
    
//拷贝构造函数
//创建一个新的栈对象，其内容与给定的栈对象 stk 相同
stack(const stack &stk);

//将栈对象的内容设置为与给定的栈对象 `stk` 相同，并返回当前栈对象的引用。
stack& operator=(const stack &stk);

//将元素 `elem` 添加到栈的顶部
push(elem);

//从栈的顶部移除第一个元素
pop();

//返回栈顶元素，但不对栈进行修改
top();

//判断栈是否为空，如果栈为空则返回 true，否则返回 false
empty();

//返回栈的大小，即栈中元素的个数
size();
```
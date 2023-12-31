## 一、基本介绍
### 1.1 Linux
- 文件目录
- 基本操作命令
- vim 基本操作命令

## 二、编译过程
### 2.1 C 语言编译
- 预编译
把 .c源文件编译成 .i 预处理文件
```shell
    gcc -E [源文件.c] -o [自定义名.i]
```

- 编译成汇编语言
把 .i 文件编译成 .s 汇编语言文件
```shell
gcc -S [源文件.c] 
```
- 注意：隐藏了预编译、删除预处理i文件的过程

- 编译成二进制
把 .s 编译成二进制.o 文件
```shell
gcc -c [源文件.c] -o [自定义文件名.o] [编译选项]
```
- 注意：隐藏了。。。

- 链接成可执行文件
把 .o 文件，链接成可执行的二进制文件
```shell
gcc [.o] -o [自定义文件名] [链接选项]
```

### 2.2 C++ 语言编译
- 预编译
把 .c源文件编译成 .ii 预处理文件
```shell
gcc -E [源文件.c] -o [自定义名.ii]
```
- 编译成汇编语言

把 .i 文件编译成 .s 汇编语言文件
```shell
gcc -S [源文件.c] 
```
- 注意：隐藏了预编译、删除预处理i文件的过程

- 编译成二进制
把 .s 编译成二进制.o 文件
```shell
gcc -c [源文件.c] -o [自定义文件名.o] [编译选项]
```
- 注意：隐藏了。。。

- 链接成可执行文件
把 .o 文件，链接成可执行的二进制文件
```shell
gcc [.o] -o [自定义文件名] [链接选项]
```

## 三、GCC

## 四、Makefile

### 4.1 基础语法
```makefile
target : prequisties
    @command
```

### 4.2 变量使用
先赋初值，调用语法如下：
```makefile
$(变量名)
```

### 4.3 函数
#### shell
- 使用Linux命令

#### patsubst
- 按照一定的模式替换字符串

#### subst
- 直接替换字符串

#### dir 
- 取父级目录

### 4.4 其它
1. 增加编译选项的方法
```makefile
include_paths := /datav/Lean/opencv4/include/opencv4 \
                 /datav/Lean/OpenBLAS/include

I_option := $(include_paths:%=-I%)
```

2. 伪目标.PHONY
告诉 Make 在.PHONY 后面的都是伪目标（命令），不用生成文件，每次都会执行下面的 command（如果有 command 的话）


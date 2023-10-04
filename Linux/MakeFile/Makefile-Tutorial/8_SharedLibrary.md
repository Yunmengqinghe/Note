## 一、编库
+ 编译 .c 文件
源文件[.c/cpp] -> Object文件[.o]
```makefile
g++ -c [.c/cpp][.c/cpp]... -o [.o][.o]... -I[.h/hpp] -g -fpic
```

Object文件[.o] -> 动态库文件[lib库名.so]
```shell
g++ -shared [.o][.o]... -o [lib库名.so] 
```

main文件[.c/cpp] -> Object文件[.o]
```shell
g++ -c [main.c/cpp] -o [.o] -I[.h/hpp] -g
```

## 二、链接
+ 链接 main 的 Object 文件与动态库文件[lib库名.so]
```shell
g++ [main.o] -o [可执行文件] -l[库名] -L[库路径] -Wl,-rpath=[库路径]
```
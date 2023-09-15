## 一、创建项目
1. 创建项目时路径不能有中文
2. 要手动在CMakeList.txt中手动添加资源文件
```txt
set(PROJECT_SOURCES
        main.cpp
        dialog.cpp
        dialog.h
        dialog.ui
        res.qrc
)
```
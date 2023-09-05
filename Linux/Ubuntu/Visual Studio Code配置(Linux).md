## 一、安装与打开
1. 使用Ubuntu SoftWare下载安装
2. 打开方式
	+ 将Visual Studio Code添加到收藏区打开
	+ 使用终端输入`code .`打开

## 二、VS Code配置
### 编译器配置
1. 使用
`sudo apt-get update`
2. 安装Vim
`sudo apt-get install vim`
3. 安装gcc
`sudo apt install gcc`
4. 安装g++
`sudo apt install g++`
5. 安装gdb
`sudo apt-get install gdb`

### 文件与工作区
1. 在文件 -> 打开文件夹，将存储代码的文件夹导入VS Code中
2. 将新文件添加到工作区：将写的不同语言(c与cpp)文件，添加到工作区，可以实现使用多种语言切换
3. 创建、打开工作区的文件即可编程

### 插件安装
1. 插件搜索快捷键
`Ctrl+Shift+X`

2. 安装`C\C++` 、`C\C++ Extention Pack`、`C\C++ Themes`、`Chinese(Simplified)`插件

### 字体与代码格式化
1. 字体设置：
	+ 文件 -> 首选项 -> 文本编辑器 -> 字体
	+ `Font Family`修改字体为`Consolas`
	+ `Font Size`修改字体大小

2. 设置分号格式化代码：
	+ 文件 -> 首选项 -> 文本编辑器 -> 格式化
	+ 选择`Format On Paste`、`Format On Type`
	+ 搜索`C_Cpp:Formatting`，选择`vcFomat`

### 多文件编译问题
1. `.cpp`多文件配置
```json
{
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: g++ 生成活动文件",
            "command": "/usr/bin/g++",
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                
                //"${file}",
                //替换 "*.cpp",
                "*.cpp",
                
                "-o",
                
		//"${fileDirname}/${fileBasenameNoExtension}"
		//替换"${fileDirname}/a.out"
                "${fileDirname}/a.out"
                
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "调试器生成的任务。"
        }
    ],
    "version": "2.0.0"
}
```

2. `.c`多文件配置
```json
{
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: gcc 生成活动文件",
            "command": "/usr/bin/gcc",
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                
                //"${file}",
                //替换
                "*.c",
                
                "-o",
		
		//"${fileDirname}/${fileBasenameNoExtension}"
		//替换
                "${fileDirname}/a.out"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "调试器生成的任务。"
        }
    ],
    "version": "2.0.0"
}
```

## 三、删除VS Code
1. Ubuntu Software删除Code
2. 终端`ll`查看文件
3. 终端`rm -rm .vscode`删除所有文件
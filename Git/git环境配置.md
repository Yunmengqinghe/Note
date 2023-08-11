## 一、下载
1. https://git-scm.com
2. 在桌面单击右键显示==git==相关程序则下载完成

## 二、基本配置
1. 打开Git Bash设置名字与邮箱
`git config --global user.name "<name>"`
`git config --global user.email "<email>"`
2. 查看配置
`git config --global user.name`
`git config --global user.email`

## 三、为常用指令配置别名
1.在用户目录下创建`.bashrc`文件
`touch ~/.brahrc`
2.在`.bashrc`文件下输入指令：
```
#用于输出git提交日志
alias git-log=='git log --pretty=oneline -- all --graph --abbrev-commit'
#用于输出当前目录所有文件及基本信息
alias ll='ls -al'
```
3. 执行配置
`soure ~/.brshrc`
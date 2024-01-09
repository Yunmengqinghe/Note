## 一、获取本地仓库
1. 在磁盘创建一个空文件夹作为本地仓库
2. 在目录下使用右键打开执行`git init`
3. 创建成功则目录下有隐藏的`.git`目录

## 二、基础操作指令
1. Git工作目录下对于文件的修改(增加、删除、更新)会存在几个状态，这些修改的状态会随着我们执行Git的命令而发生变化。
![[Git Work Directory.png]]
2. 指令
```
1.
git add //从工作区添加到暂存区
git add . //将所有目录都加入暂存区

2.
git commit -m "<注释>"//从暂存区添加到仓库

3.
git status //查看文件的状态

4.
git log[option] //查看提交记录
git -log //之前的配置，包含以下几种新式
option:
	--add //显示所有分支
	--pretty=oneline //将提交信息显示为一行
	--abbrev-commit //使输出的commit更简短
	--graph //以图表的形式显示

5.
git config --global core.autocrlf true
//Git 可以在你提交时自动地把回车（CR）和换行（LF）转换成换行（LF），而在检出代码时把换行（LF）转换成回车（CR）和换行（LF）

6.
git diff
//显示修改的地方
```

## 三、版本回退
1. 作用：版本切换
2. 命令形式
+ `git reset --hard commitID //commitID可以使用git -log或git log查看`
3.如何查看已经删除的指令
+ `git reflog //可以看到已经删除的提交记录`

## 四、添加文件到忽略列表
+ 一般我们总会有些文件无需纳入Git 的管理，也不希望它们总出现在未跟踪文件列表。通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。在这种情况下，我们可以在工作目录中创建一个名为.gitignore 的文件(文件名称固定) ，列出要忽略的文件模式。下面是一个示例:
```
# 忽略 .a 文件
*a
# 即使忽略了上面的.a文件,但是要跟踪lib.a，
!lib .a
# 仅忽略当前目录中的 ToDo 文件，而不忽略 subdir/ToDo
/ToDoTODO
# 忽略构建/目录中的所有文件
buid/
# 忽略 doc/notes .txt，但不忽略 doc/server/arch.txt
doc/*,txt
# 忽略 doc/ 目录中的所有.pdf文件
doc/**/*.pdf
```
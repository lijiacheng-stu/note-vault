## 基础知识
1. git 三个主要的部分：工作目录(working directory)、 暂存区(staging area)、git仓库(git repository)， 这是查看状态的关键
2. 存在两类状态：working diretory 相对于staging area的状态；staging area 相对于 git repository的状态；
3. git 配置的三个区域：系统级、用户级、仓库级 （--system, --global, --local）, 后面会覆盖前面的配置
	- 配置项：
		- Your Identity：每个Git提交都使用这些信息
		- Your Editor
		- 代理 http.proxy / https.proxy
	- 增删改查
		- 查：`git config --list --show-origin`
		- 其他：查ai，或者 `git config --help`



git的使用场景是什么呢？


## 类别一：本地的版本控制
本地的版本控制需要掌握的使用场景
1. 完成一次提交
2. 在
3. 
4. 创建新的分支，实现分支间的切换
5. 

### 对1
### 1.1 查看对文件的状态
初始状态： 分支指向git repository中的一个commit，staging area和working directory与这个commit完全一样


## 类别二： 本地与github仓库之间的同步
1. 将本地文件夹push到github仓库


## 类别三：通过仓库之间的联动，实现写协作开发

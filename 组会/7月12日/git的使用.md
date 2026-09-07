## 基础知识
1. git 三个主要的部分：工作目录(working directory)、 暂存区(staging area)、git仓库(git repository)
2. git status会根据三个部分两两之间的差异，输出两类状态：working diretory 相对于staging area的状态, 记为状态1；staging area 相对于 git repository的状态，记为状态2；
3. git 配置的三个区域：系统级、用户级、仓库级 （--system, --global, --local）, 后面会覆盖前面的配置
	- 配置项：
		- Your Identity：每个Git提交都使用这些信息
		- Your Editor
		- 代理 http.proxy / https.proxy
		- init.defaultbranch
	- 增删改查
		- 查：`git config --list --show-origin`
		- 其他：查ai，或者 `git config --help`

4. 对每个文件的内容创建blob，为每个目录窗间tree，为每个commit创建commit。commit指向项目根目录的tree，指向父commit。
![[Pasted image 20260714142438.png]]
![[Pasted image 20260714142448.png]]

5. branch是指向commit object的指针，HEAD是指向branch的指针


git的使用场景是什么呢？


## 类别一：本地的版本控制
本地的版本控制需要掌握的使用场景
1. 完成一次提交
2. 分支管理
3. 

### 对1
#### 1.1 查看文件的状态
指令： `git status` 或`git status -s` 
切换文件状态：`git add `
初始条件： 指向git repository中的一个commit，staging area和working directory与这个commit完全一样。此时，所有文件都是unmodified。
状态1和状态2是由文件状态构成的。
- 状态1：
	- 文件状态：tracked管的是`working directory中，是否存在staging area中不存在的文件`，存在就是untracked, 不存在tracked；staged管的是staging area中存在的文件，working directory 和staging area中两者是否相同，相同就是staged, 不同就是unstaged; 不同的方式有很多，可以分类为modified、deleted等等。
		![[Pasted image 20260714115449.png]]
	- git add实现任意其他状态，转化成tracked中的staged状态。staged状态下，不会显示状态1。
	- 存在一种特殊的状态，一个文件两个都相同，就是unmodified。
- 状态2
![[Pasted image 20260714122328.png]]

#### 1.2 查看三个部分之间的具体修改的细节
指令：
- `git diff` :查看working directory 和staging area
- `git diff --staged`：查看staging area和最后一次提交

#### 1.3 撤回修改
指令：
- `git restore --staged <file>` ，用git仓库恢复staging area
- `git restore <file>`， 用staging area恢复working directory


#### 1.4 完成一次提交
`git commit -m ‘commit message’`
#### 1.5 查看提交记录
指令:
- `git log`
- `git log --oneline --graph --all`
	- graph是展示分支，以及合并记录
	- oneline是用一行展示一次提交

### 对2
#### 2.1 基础
1. 查：`git branch`
2. 增：`git branch testing`
3. 删




#### 2.3 分支切换
含义：让HEAD从branch1，指向branch2
`git switch branch2` // 新版本推荐
`git checkout branch2`

创建并切换
`git switch -c branch2`
`git checkout -b branch2`




2.3 分支合并





## 类别二： 本地与github仓库之间的同步
1. 将本地文件夹push到github仓库


## 类别三：通过仓库之间的联动，实现写协作开发

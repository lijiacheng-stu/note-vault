You'll create your own Hello World repository and learn GitHub's pull request workflow, a popular way to create and review code.
- create repository
- create a branch
创建repository
![[Pasted image 20251029214209.png]]
创建分支branch1，并提交commit branch1-1
![[Pasted image 20251029214904.png]]
branch1向main发起PR， main上合并
![[Pasted image 20251029215453.png]]
在branch1上branch2：
![[Pasted image 20251029215740.png]]

branch1提交branch1-2；brach2提交branch2-1：
![[Pasted image 20251029215942.png]]
 branch2向branch1发起pull request，并merged commit
 ![[Pasted image 20251029220323.png]]
产生了两个认识:
- 看一个commit的父节点,就可以知道这个commit的来由
- 疑问:提交和被提交的分支,最后一定要相同
![[Pasted image 20251029221936.png]]
不同用户存在冲突的合并,是否会同步修改?
创建li创建repository
![[Pasted image 20251029223503.png]]


**一个Git项目的三个主要的区域** 
![[Pasted image 20251030131035.png]]
If a particular version of a file is in the Git directory, it’s considered committed. If it has been modified and was added to the staging area, it is staged. And if it was changed since it was checked out but has not been staged, it is modified. In Git Basics, you’ll learn more about these states and how you can either take advantage of them or skip the staged part entirely.

- .git directory: 核心内容是所有的commit，以及git log graph
- staging area: 存储“将进入下一个commit的内容”信息。换句话说，当前staging area的中的文件是什么样，那么如果提交commit的话，commit中的内容就会是怎样的。
- Working Dietory：初始状态下，会是项目的所有commits中的一个版本。可以增删改文件。


那这些区域怎么联动起来呢？
对working directory中的文件建立文件状态的标签：untracked, unmodified, modified,staged。


初始状态：
- working directory：初始状态下，会是项目的所有commits中的一个版本。并对所有文件都标记为unmodified。
- staging area: 与working directory中，一样的版本，且所有文件都标记为committed或者是unmodified


unmodified表明，该文件是在staging area且是committed（文件与上一个版本相同），在working diretory中是保持原样的。modified表明，该文件在staging area且是committed状态，而在working directory中的版本已经发生了改变。 staged表明，该文件在staging area是modified状态，且在working direcotory中也是修改了的状态。

utracked是该文件在working directory中是添加状态，但是在staging area是没有该文件的状态。




**文件状态的生命周期**
![[Pasted image 20251030131814.png]]




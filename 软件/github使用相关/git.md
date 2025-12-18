### 快捷键
#### vim编辑器下
[vim的三种模式-CSDN博客](https://blog.csdn.net/GoodLinGL/article/details/123971139?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171353469316800215031287%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=171353469316800215031287&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-123971139-null-null.142^v100^control&utm_term=vim%E7%9A%84%E4%B8%89%E7%A7%8D%E6%A8%A1%E5%BC%8F%E6%80%8E%E4%B9%88%E5%88%87%E6%8D%A2&spm=1018.2226.3001.4187)


### 常用的非git命令
- `ll` 
查看文件夹下的所有文件
- cat 文件名
查看文件内容
### 常用的git命令
![[Pasted image 20240419213514.png]]

- git config --global --list
能够查看用户签名的信息，信息存储在"C:\Users\李嘉成\.gitconfig"
**注意：**
- git init
初始化本地库，就是在当前文件下创建.git文件夹
由于git是linux开发的，所以cd切换目录的时候，/是斜杠不是反斜杠\
- git reflog
查看精简版的日志记录
![[Pasted image 20240419221618.png]] 
- git log
详细版的日志信息
#### 分支
![[Pasted image 20240419222800.png]]
- git branch -v
能够查看当前的分支数量，以及正处于的分支
![[Pasted image 20240419223758.png]]
分支的底层逻辑
head指向分支，分支指向具体版本。
当前指针指向的那个分支所指向的版本就是当前能够查看的版本。
在某个版本创建了某个分支，当提交后，只能指向那个版本的那个。
![[Pasted image 20240419225138.png]]
### 如何理解状态之间的切换



### 线索得出的结论
实验内容：对`git add`后的文件进行修改，最后再提交，观察git add到git commit之间的修改是否保存到版本库中？
实验结论：会保存到版本库。

实验内容：观察reflog信息，与文件中的关联？
- 从日志中得到的信息
简略版：
e9eb857 (HEAD -> hot-fix) HEAD@{0}: commit: hox-fix student after add
完全版：
```
commit e9eb857ce7722e63b8296ed885fe3d21a216d653 (HEAD -> hot-fix)
Author: gary <2477492942@qq.com>
Date:   Sat Apr 20 15:05:47 2024 +0800

    hox-fix student after add
```
- 在文档中的信息
在head文件中：
ref: refs/heads/hot-fix
在hot-fix文件中：
e9eb857ce7722e63b8296ed885fe3d21a216d653
结论：
head 指向分支，分支指向版本。




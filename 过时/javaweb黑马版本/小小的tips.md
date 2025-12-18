#### 1.查询mysql所占用的端口号
- `mysql -uroot -p123456` 
登录mysql
- show global variables like 'port' ;
查看Port变量
![[Pasted image 20240410150501.png]]


#### 2.手工制造异常集锦：
- mysql
随便写一个非sql语句
```sql
update account set money=money-500 where name='小亮';
我是猪...
update account set money=money+500 where name='小张';
```
- java
除一个0就行
```java
sout("hello");
int a=3/0;
sout("world!");
```


#### 3.查询所有端口号的方法
![[Pasted image 20240414151128.png]]

#### 4.根据pid查询进程
- 打开任务管理器
- 打开pid的显示列
- 根据pid找到相应进程
![[Pasted image 20240414161337.png]]
#### 5.关闭占用指定端口号的进程
- 打开cmd
- 输入`netstat -ano`,查找对应端口号的进程号
	- 进阶做法通过管道 `netstat -ano|findstr "keyword"`
- 打开任务管理器，找到对应的进程号的进程，关闭进程
#### 6.设置应用的默认打开方式
![[Pasted image 20240414165755.png]]
#### 7.新版idea中部署一个web项目方法
#### 8.修改文档模板并添加到鼠标右键New中
**添加的目标位置：** 
![[Pasted image 20240416171005.png]]
**步骤** 
- file->setting->搜索框输入 File and Code Templates
![[Pasted image 20240416171136.png]]
- 在other中有标准的模板，选定最符合自己要求的模板
![[Pasted image 20240416171258.png]]
- 在Files中点击+,将模板体粘贴到里面新建的里面去，并进行一定的改装。



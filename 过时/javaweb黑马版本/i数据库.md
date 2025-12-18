## 概念
![[Pasted image 20240408154442.png]]
数据库是概念，数据库软件是概念的实现
## MySQL数据库软件：服务
### 安装卸载和配置
![[Pasted image 20240408162234.png]]
注意：
- 本质上就是打开服务界面（services.msc），找到mysql服务，关闭或启动。下载MySql也其实是下载mysql服务
- 我下载的版本是：Server version: 8.0.29 MySQL Community Server - GPL
![[Pasted image 20240408160706.png]]

### 目录结构
![[Pasted image 20240408163243.png]]



## SQL
### 概念、通用语法、SQL语句分类
![[Pasted image 20240408164444.png]]
**sql语言分类的图形化描述** 
![[Pasted image 20240408164510.png]]
### DDL：CRUD数据库和表
#### 操作数据库：CRUD+使用 
- CR
![[Pasted image 20240408165719.png]]
- ud+使用
![[Pasted image 20240408170800.png]]

注：
- use 数据库名称;
作用是进入数据库，便于后续对表的操作
- CRUD
只表示操作类型，不表示操作时使用的关键字
C create 创建 
R retrive 获取
U update 更新
D delete 删除
#### 操作表：CRUD
##### c
![[Pasted image 20240408172225.png]]
![[Pasted image 20240408173935.png]]
![[Pasted image 20240408172444.png]]
```sql
create table student(
	id int,
	name varchar(32),
	age int,
	scores int,
	birthday date,
	insert_time timestamp
);
```
注：
- 创建一张表，就是指定表明，已经表中每一个列，以及每个列的约束

##### RUD
- R
![[Pasted image 20240408173723.png]]
- D
![[Pasted image 20240408174013.png]]
- U
![[Pasted image 20240408174432.png]]

### DML：增删改表中的数据
#### 增加数据
![[Pasted image 20240409174329.png]]


#### 删除数据
![[Pasted image 20240409174807.png]]
#### 修改数据
![[Pasted image 20240409175047.png]]


### DQL1：查询表中的数据（对单表的查询）
#### 语法结构
![[Pasted image 20240409193308.png]]

#### 基础查询：select，from，多列的查询
![[Pasted image 20240409180120.png]]
#### 条件查询:where 关系（><）、逻辑(and or not)、模糊(like _ %)
![[Pasted image 20240409184452.png]]
注：
- between and 用以替换一个属性介于两值之间的情况，简化代码,包含边界
age>=18 and age<=30 等价于 age between 19 and 30;
- in 用于或的情况
age=18 or age=30 or age=12 等价于 age in (18,30,12);
- age is NULL 或 age is not NULL ，用于判断空值
age=NULL ,这种判断不了，因为null特殊
- like是模糊查询，通过以下案例熟悉：
姓马的人：` name like "马%"`
第二个字是马的人：` name like "_马%"`
包含马字的人：`name like “%马%”`



#### 排序查询order by
![[Pasted image 20240409190316.png]]
#### 聚合函数（sum,avg,max等，出现在select后，或者having后）
![[Pasted image 20240409190843.png]]


注：聚合函数中的cout用于统计班级里的人数，如果存在null，那么count将会出现误差，为了解决这个问题，两种解决方案
- 方案一：统计非空列
`count(id) ;//id是作为主键，绝对非空`
- 方案二：ifnull函数
`count(ifnull(english,0));//相当于把非空给去除了` 
#### 分组查询(group by,having,聚合函数)
![[Pasted image 20240409191858.png]]
按照下面的例子逐步深入：
- 查询男女数学平均分和人数
```sql
select sex,avg(math),count(id)  -- sex分组字段，avg()是聚合函数
from student 
group by sex;
```
- 只将分数大于70分的人纳入上面的统计
```sql
select sex,avg(math),count(id)
from student
where math>70 //在分组之前进行了限定，将不满足的部分排除在分组之外
group by sex;
```
- 将分组后人数大于2的进行展示
```sql
select sex,avg(math),count(id)
from student
where math>70 //在分组之前进行了限定，将不满足的部分排除在分组之外
group by sex
having count(id)>2;
```



#### 分页查询（limit 方言）
![[Pasted image 20240409193109.png]]

### 约束
#### 概念与分类
![[Pasted image 20240409195502.png]]
- **key words:** 正确性、有效性和完整性
- 描述一个约束，应该**包含** ：
	- 这个约束的效果
	- 如何增加这个约束（创建表时，表创建后如何添加）
	- 如何删除这个约束
#### 非空约束 not null
![[Pasted image 20240409195824.png]]
#### 唯一约束 unique
![[Pasted image 20240409195919.png]]
注意：
- 如果借鉴not null的方法删除唯一约束是会显示运行成功，但是没效果
```sql
alter table stu modify phone_number vachar(20); --错误，能运行但无效
alter table stu drop index phone_number; --正确，有效
```

#### 主键约束：primary key
![[Pasted image 20240409201021.png]]
##### **自动增长：** 往往和主键一起使用
![[Pasted image 20240409201233.png]]
**效果**
- id被auto_increment约束，当插入的数据id属性为Null时，按照前一条数据自动增加1，不会成为空值。当插入的数字为具体的数字时，按照插入的数据插入，并在递增的序列中。



#### 外键约束：foreign key 
**引入**
**外键约束** ：当一个属性重复出现，出现数据冗余时，修改冗余数据容易出现修改不全的情况，而且很占据内存空间，这个时候可以将容易数据压缩成一个表，然后原表引用新表的对应值就行。作为索引连接连个表之间的属性名（列名），就是外键，勾连的语句就是外键约束。
![[Pasted image 20240409203353.png]]
**效果：**
- **自定义** ：有foreign key语句的叫做**关联表** ，另外一个叫 **被关联表** 
- **效果** ：
	- 向关联表中添加数据时，关联表中相应的字段要么是null，要么就得保证被关联表中含有这样的字段
	![[Pasted image 20240409205632.png]]
	- 对被关联表进行删除/修改数据操作时候，如果相应的字段被关联，那么这个字段无法被删除/修改
	![[Pasted image 20240409205222.png]]
	- 被关联表至少是unique修饰的
**问题** 
	- 当被关联表相关字段要发生改变的时候，必须从关联表开始改起，然后才是被关联表，非常麻烦容易出错-->级联操作
	
	![[Pasted image 20240409211135.png]]

### 数据库的设计
#### 多表之间的关系
##### 分类
![[Pasted image 20240409211652.png]]
##### 实现关系
###### 文字小结
![[Pasted image 20240409213153.png]]
###### 一对多
![[Pasted image 20240409212736.png]]
![[Pasted image 20240409212713.png]]
###### 多对多
![[Pasted image 20240409212933.png]]
![[Pasted image 20240409212907.png]]

###### 一对一
![[Pasted image 20240409213044.png]]
![[Pasted image 20240409213017.png]]
- 注：这种情况很少，既然是一对一，为什么不合成一张表呢
![[Pasted image 20240409213124.png]]
###### 应用举例
![[Pasted image 20240409213955.png]]

#### 数据库设计的范式
##### 相关知识点的记录
![[Pasted image 20240409221512.png]]
##### 课程的思路与记录
**1.普通的表如下**
![[Pasted image 20240409221323.png]]
问题：系这一列是可以分割的原子项，不符合第一范式
**2.解决不符合第一范式的问题后，成为以下表格** 
![[Pasted image 20240409221555.png]]
增删之后的表格如下：
![[Pasted image 20240409222048.png]]
对表的依赖关系进行分析：
		学号-->(姓名，系，主任) 
		系-->主任
		(学号，课程名称)-->(分数)
	所以码就是（学号，课程名称）
	非主属性 （分数，姓名，系，主任）
	其中 姓名，系，主任部分函数依赖于(学号，课程名称)
**3.消除部分函数依赖后得到的表：**
![[Pasted image 20240409222709.png]]
增删之后的表格如下：
![[Pasted image 20240409222828.png]]
对表中依赖的分析：
	表一：
		学号-->(课程名称，分数)
	表二：
		学号-->(姓名，系名，系主任)
		系名-->系主任
	所以符合不存在非主属性对主属性的部分函数依赖了，但是存在系主任对学号的传递函数依赖

**4.消除传递函数依赖：**
![[Pasted image 20240409223356.png]]
增删之后的表格如下：
![[Pasted image 20240409223521.png]]

![[Pasted image 20240409223540.png]]








### DQL2:多表查询
#### 笛卡尔积

![[Pasted image 20240409224116.png]]
#### 多表查询分类

##### 内连接查询
**隐式内连接** 
![[Pasted image 20240410090240.png]]
**显示内连接** 
![[Pasted image 20240410090553.png]]

##### 外连接查询
![[Pasted image 20240410091053.png]]

###### 注：内连接和外连接的区别
stu 表
![[Pasted image 20240410093557.png]]
dept 表
![[Pasted image 20240410093707.png]]
需求：查询所有学生名字，及其所在部门：
**内连接** 
```sql
select stu.name,dept.department
from stu,dept
where stu.dept_id=dept.id;
```
![[Pasted image 20240410093904.png]]
结果分析：将dept_id为null的小光给去除掉了
**左外连接** 
```sql
select stu.name,dept.name
from stu left join dept
on stu.dept_id=dept_id;
```
![[Pasted image 20240410094238.png]]
总之：内连接会将连接属性为Null的去除掉，左外连接会将坐标的全部信息保留，为null的后面的表的情况也为null

##### 子查询
![[Pasted image 20240410094541.png]]


### 事务transaction
**引入：**
小明给小亮转账500块钱时，数据库进行的操作：
 - 判断小明的余额大于500
 - 小明的金额-500
 - 小亮的金额+500
 在这个操作中，如果在第二步出现异常，那么小明-500但小亮的金额却不变，这样500不翼而飞，是危险的操作。如果这三步同时成功，或者同时失败就好了。-->事务transaction
 **知识点** 
 基本介绍
![[Pasted image 20240410100823.png]]
![[Pasted image 20240410101659.png]]
四大特征：
![[Pasted image 20240410103037.png]]
个人理解：
- 开启事务（start transaction）后，其实是打开了一个数据库的副本，对这个副本上的任何操作，都不会影响到原来的数据库
- 提交事务（commit）后，就将副本的内容成为了真实数据库的内容
- 回滚事务(rollback)后，把数据库还原到开启事务前，相当于删除当前副本，并创建新的副本，新的副本自然和原数据库一样
- 安全原理：先测试再提交，这肯定是非常安全的。
###### **例子**
![[Pasted image 20240410101516.png]]
![[Pasted image 20240410101602.png]]


### DCL
#### 管理用户：增删查用户，修改密码
![[Pasted image 20240410104543.png]]
![[Pasted image 20240410104610.png]]
**操作的本质：** 对mysql数据库下user表进行修改或者查询。但是往往不是直接修改，而是通过Mysql内置的sql语句进行修改。
![[Pasted image 20240410104739.png]]

#### 管理权限：查询，授予与撤销权限
![[Pasted image 20240410105550.png]]
## JDBC
### JDBC的概念、快速入门、各个类的详细解释、事务
#### 概念
![[Pasted image 20240410110613.png]]
![[Pasted image 20240410110553.png]]
接口已经再java的api文档中，但是对应的实现类却没有，所以得下载相应的实现类，这些实现类就是数据库驱动。
#### 快速入门
![[Pasted image 20240410145948.png]]
![[Pasted image 20240410150015.png]]



#### 详解各个对象
![[Pasted image 20240410180442.png]]
- DriverManager
	![[Pasted image 20240410152830.png]]
**作用1**：告诉程序使用哪儿一个数据库驱动jar
通过`Class.forName("com.mysql.jbc.Driver")` 语句实现，本质是调用静态代码块中的内容。
现在已经不用写了，自动会弄。
![[Pasted image 20240410153352.png]]
**作用2**：获取数据库连接
告诉程序连接哪儿个数据库。
- Connection
![[Pasted image 20240410153624.png]]
注：需要释放资源
- Statement
![[Pasted image 20240410154104.png]]
注：定义的sql不需要加分号
需要释放资源
- ResultSet
![[Pasted image 20240410161710.png]]
![[Pasted image 20240410161732.png]]
注：游标的初始位置在第一行之前。next()返回值boolean，如果在最后一行之后，返回false，否则返回true。
需要释放资源
- PreparedStatement
以后都得用PreparedStatement而不是Statement。前者效率更高也更安全。
![[Pasted image 20240410221407.png]]

#### JDBC控制事务
![[Pasted image 20240410223135.png]]
注：执行前，开启事务； 实行到末尾还没有出现异常，提交事务；发生异常，回滚事务。
仍然可以以小明给小亮转账500块钱为例进行。
### 数据库连接池(DataSource)
#### 概念、好处、实现
![[Pasted image 20240410225520.png]]
#### c3p0
![[Pasted image 20240411081602.png]]
配置文件的标准名称：
- c3p0.properties 
- c3p0-config.xml
#### druid(重点掌握)
![[Pasted image 20240411090345.png]]
- 获取DruidDataSourceFactory的对象的d实际操作
![[Pasted image 20240411091257.png]]
- driud.properties的配置信息
![[Pasted image 20240411090453.png]]

### Spring JDBC
![[Pasted image 20240411153345.png]]
![[Pasted image 20240411153412.png]]
导包：
![[Pasted image 20240411101547.png]]

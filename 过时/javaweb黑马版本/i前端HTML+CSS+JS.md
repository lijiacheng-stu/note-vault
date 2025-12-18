## web概念概述
**软件架构** 
![[Pasted image 20240411154328.png]]
学习的是BS架构
**资源分类**
![[Pasted image 20240411155411.png]]
![[Pasted image 20240411155328.png]]





## HTML（标签与重要属性）
### 概念和快速入门
**该文件夹下面有有标签文档：** 
"F:\resouceAndDependence\www.w3school.com.CHM"
![[Pasted image 20240411160749.png]]
### 标签学习1（标签+重要属性）
#### 概览
![[Pasted image 20240411162634.png]]
#### 特殊字符表
![[Pasted image 20240411170109.png]]
#### 文件标签
![[Pasted image 20240411164038.png]]
注：idea中创建html文件会自动生成
#### 文本标签
![[Pasted image 20240411170312.png]]
**属性定义方法** ：颜色，宽度、对其方式
![[Pasted image 20240411170518.png]]
![[Pasted image 20240411170728.png]]



#### 图片标签
![[Pasted image 20240411174811.png]]
**引用资源之相对路径**
![[Pasted image 20240411172939.png]]
#### 列表标签
![[Pasted image 20240411173533.png]]

#### 链接标签
![[Pasted image 20240411174122.png]]
**应用**
图片+超链接实现点击图片跳转页面
#### 块标签和语义化标签
![[Pasted image 20240411174628.png]]
特点：
- 没有样式，方便配合css使用
- 语义化标签为了提高代码的可读性而已


#### 表格标签
![[Pasted image 20240411180249.png]]
![[Pasted image 20240411175123.png]]

### 标签学习2（表单标签）
####  表单的概念与form标签
![[Pasted image 20240411211741.png]]
#### input标签
![[Pasted image 20240411213434.png]]
![[Pasted image 20240411213416.png]]
![[Pasted image 20240411213450.png]]
注意：
label标签能够让点文字也会点击那个框 for=”结合的那个框的id“

#### select标签和文本域
![[Pasted image 20240411214018.png]]
![[Pasted image 20240411213919.png]]
![[Pasted image 20240411214037.png]]
![[Pasted image 20240411214047.png]]


























## CSS（选择器与重要属性）
### 概念\好处\css核心语法
![[Pasted image 20240411223737.png]]
![[Pasted image 20240411225425.png]]

### CSS与html结合方式
**概览**
![[Pasted image 20240411224400.png]]
**内联样式与内部样式**
![[Pasted image 20240411224445.png]]
**外部样式**
![[Pasted image 20240411224601.png]]



### 选择器
#### 基础选择器
![[Pasted image 20240411230149.png]]
#### 扩展选择器 
![[Pasted image 20240412170423.png]]


### 属性
![[Pasted image 20240412170904.png]]
**盒子模型**
![[Pasted image 20240412171648.png]]
![[Pasted image 20240412171630.png]]











## JavaScrip
### 概念，功能，发展史
![[Pasted image 20240412174559.png]]
### ECMAScrip
#### 预备知识
##### 函数
- `document.write()`
write里面双引号中的内容时可以有标签的，而且标签会生效
- `alert()`
- typeof() 运算符
##### 特殊地语法
![[Pasted image 20240412205539.png]]
#### 基本语法
##### 与html的结合方式
![[Pasted image 20240412175322.png]]
##### 注释与数据类型
![[Pasted image 20240412175813.png]]
![[Pasted image 20240412180107.png]]
注意：
- js没有文档注释
##### 变量
![[Pasted image 20240412182750.png]]
需要掌握的
- js是弱类型语言
- js中变量的定义var a=3;
- 通过typeof()获取变量类型

##### 运算符
###### 概览与心得总结
算数，关系，逻辑，赋值，其他（三元运算符，一元运算符）
![[Pasted image 20240412195905.png]]
可能时由于javaScript不是一种语法特别严格地语言，以任意数据类型带入，都能够根据转换关系，得出正确确定地结论
###### **以java为参照物，梳理与java不同的使用情况**
- 一元运算符之+（正号） 也有对应的-（负号） 
本质上时，当一个位置需要number类型，但填了其他类型时，怎么转成number的
`+a`
当a为number时，返回值为a的数值，a为NaN时，结果为NaN
当a为string时,若string内容能被解析成数值，返回值为解析后的数值，否则为NaN
当a为boolean时，false为1，true为0
当a为null时，为0
当undefined时，为NaN
- 算数运算符之 /(除)
这里不像java和C中属于整除，而是除到小数点的。`3/5=0.6`
结合上述中数值转换进行进一步理解
- 比较运算符 > ,< ,== ,===
当比较的类型相同时，
	number时，直接比较，判断。当参与者有NaN时，一定返回false
	string时，按照字典顺序，从头到尾，知道出现一个比出来（可能是根据字符集的位置吧）
	Boolean时，与将true代为1，false代为0，比较出来的结果一样
	null时，与将null代为0时，比较出来的结果一样
	undefined时，大于小于均为false,== 或=== 时为true
当比较的类型不同时，
	都是转成其对应数字后进行比较。特别地，对于=== 先判定类型再作比较
- 逻辑运算之！
	number时，非0为true，0为false
	string时，空字符串“”为false，其他均为true
	boolean时，不需要讨论
	null时，false
	undefined，false
	object时为true
	
	
	
 


##### 流程控制语句
和java时一样的
![[Pasted image 20240412205850.png]]
![[Pasted image 20240412205929.png]]


#### 基本对象
##### 概览
对于对象的学习，关注对象的创建，属性，方法（查册子），以及特点就行了。
![[Pasted image 20240412220020.png]]
- Number String Boolean就是包装类对象，下面不作具体讨论
##### Function对象
![[Pasted image 20240412212000.png]]


##### Array对象
![[Pasted image 20240412213038.png]]
##### Date对象
![[Pasted image 20240412213518.png]]

##### Math对象（不需要创建对象）
![[Pasted image 20240412213822.png]]
##### RegExp对象
###### 正则表达式（具有通用性）
关注单个字符的限定，以及量词
![[Pasted image 20240412214342.png]]
###### 正则表达式对象
![[Pasted image 20240412214825.png]]

##### Global对象（不需要创建方法，只有方法）
**方法：**
![[Pasted image 20240412222051.png]]
###### URL编码
将数据展成二进制，每1个字节转成16进制，并用%分隔离
![[Pasted image 20240412220210.png]]




DOM

### BOM
#### 概览
![[Pasted image 20240413090703.png]]
![[Pasted image 20240413090759.png]]




#### Window对象
![[Pasted image 20240413142220.png]]
![[Pasted image 20240413150911.png]]
![[Pasted image 20240413142202.png]]
#### Location对象
![[Pasted image 20240413152822.png]]

#### History对象
![[Pasted image 20240413153446.png]]

### DOM
#### Document对象
![[Pasted image 20240413154825.png]]
#### Element对象
![[Pasted image 20240413155055.png]]
#### Node对象
![[Pasted image 20240413162306.png]]
#### HTML DOM
![[Pasted image 20240413162115.png]]
## Bootstrap
了解栅格系统，框架的搭建。

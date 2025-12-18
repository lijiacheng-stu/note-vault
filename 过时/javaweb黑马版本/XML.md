## XML
### XML本身概念和语法地理解
#### 概念、功能与html的区别
![[Pasted image 20240414095802.png]]
#### 组成部分或者说是语法
![[Pasted image 20240414101604.png]]
注意：
- encoding
xml本质上是文本文件，所以存储在计算机中的编码方式就是多元的。解析引擎如何知道这个xml
的编码方法？就是得通过文档声明中的encoding属性
- version
告知的是xml的版本，不是自定义的。
- 区分大小写

#### 约束与约束的实现
##### DTD
###### 文件名与文件阅读
- 文件名: `*.dtd`
- 文档的编写之举例解读文档：-->解决了阅读的问题
![[Pasted image 20240414104537.png]]
-  ELEMENT用来声明标签元素，ATTLIST用来声明属性
- 第一行，有students标签，该标签下有student标签，0个或者多个
- 第二行，有student标签，该标签下有name,age,sex标签，且得按照顺序出现
- 第三~五行，name标签体内数据的要求是字符串
- 第六行，student下有一属性number，number的数据类型是ID(每个student的这个标签都得不一样)，必须出现
###### 引入dtd文档-->解决程序员引入的问题
**分类** 
![[Pasted image 20240414105806.png]]
**内部dtd** 
![[Pasted image 20240414105746.png]]
**外部dtd** 
![[Pasted image 20240414105713.png]]




##### Schema
###### 文件名与文件阅读
- `*.xsd`
![[Pasted image 20240414111732.png]]
- 解读：
	- 有标签，名字为students,类型是studentsType
	 - 对于studentsType这种类型是复杂类型，下面得有student元素，最少出现0次
	 - 对于student，类型是studentType
	 - 对于studentType这种类型是复杂类型，下面依次出现 name,age,sex元素
	 - name的类型是xsd:string-->只要填string就行
	 - 对于age是这种类型是简单类型，得是字符串，字符串只能在male和female中选择
###### 引入xsd文件
![[Pasted image 20240414112931.png]]
- 导入的部分在于：
![[Pasted image 20240414113344.png]]
- 第一步：引入xsi
![[Pasted image 20240414113000.png]]
- 第二步：引入约束的位置
![[Pasted image 20240414113036.png]]
两两一组，每一组中，前一个是后一个的命名空间，当要引入后一个约束时，用命名空间名称加在标签前面。
- 第三步：给命名空间加前缀
![[Pasted image 20240414113404.png]]
由于命名空间太过冗长，所以在简化一下，context就代替了后面一长串。对于直接赋值的xmlns=“”，意思就是当标签前面不加前缀时，默认采用这个。
### 在java中实现对xml的解析：Jsoup工具包
#### 以下内容讨论的范畴
xml有两种操作，一个是解析（文档中的内容导入内存），一个是写入（将内存中的数据写入文档）。由于xml写入操作目前很少涉及，所以只讲解析。
xml的解析有两种思想，DOM和SAX，由于在服务器端往往使用DOM，所以现在学习dom。sax往往用于客户端。有JAXP官方，不好用支持DOM,SAX；有DOM4J，非常优秀，但是本文Jsoup,都是dom。PULL安卓,sax
![[Pasted image 20240414114232.png]]
- 对于DOM的图形化解析
![[Pasted image 20240414114025.png]]



#### 常见的使用方式
![[Pasted image 20240414115350.png]]
![[Pasted image 20240414115435.png]]
思路：
继承关系：Document-->Element-->Node
通过Jsoup工具类，获取xml的Document对象。通过Document对象，获取想要获取的元素。在通过元素对象，获取其他的属性，文本内容，或者子元素对象。
#### 查询
![[Pasted image 20240414120925.png]]
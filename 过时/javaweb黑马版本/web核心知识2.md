### 架构与规范
#### 三层架构
![[Pasted image 20240417221631.png]]
![[Pasted image 20240417221608.png]]
#### MVC开发模式
**1.MVC模式的历史由来**
- sevlet-->jsp-->mvc
![[Pasted image 20240417130303.png]]
**2.MVC的各部分含义以及功能**
![[Pasted image 20240417130334.png]]
![[Pasted image 20240417130353.png]]
**3.MVC的优缺点**
![[Pasted image 20240417130422.png]]

#### 开发流程
![[Pasted image 20240417222332.png]]
![[Pasted image 20240417222356.png]]
#### 三层架构

### JSP
#### 概念、引入和注意点
![[Pasted image 20240417131648.png]]
以前的servlet：当页面中存在需要servlet动态生成的内容的时候，那么整个页面都得用response.getWriter().write()方法写，非常麻烦。所以引入jsp，即可以写java又可以写标签。
**注意点**
- ==JSP文件应该放在web目录下==，因为jsp直接通过虚拟目录+资源路径的形式找到，不需要像一般的servlet一样进行全类名和资源名称的匹配
#### 原理
- 当客户端服务器访问jsp资源的时候，tomcat服务器会将jsp解析成servlet。所以jsp本质上是一个servlet
![[Pasted image 20240417140215.png]]
![[Pasted image 20240417140156.png]]


#### JSP脚本
![[Pasted image 20240417140713.png]]
- 脚本2非常少用
- 脚本3也定义在serviece 方法中，但是内容是out.write()中的内容

#### 指令与注释
 **作用和格式**
![[Pasted image 20240417142006.png]]
**三类指令：page include taglib** 
![[Pasted image 20240417142131.png]]
通俗地讲：include用于包含jsp文件，taglib用于包含其他规定好地标签
**注释**
![[Pasted image 20240417142414.png]]
其实只有jsp注释，html的注释也会out.write()过去，只是浏览器解析的时候会注释掉
#### 内置对象
##### 内置对象的来历
因为jsp会转成servlet文件，这个文件里固定地声明了9个成员变量，这些成员自然就可以直接使用了。
##### 九个内置对象的名称，数据类型和作用
![[Pasted image 20240417142615.png]]
注：
- 域对象（4个）：pageContext，request，session，application
##### 对重要的内置对象的详解
###### out对象
response和out都有输出的缓冲区，tomcat会先去找response的缓冲区，再去找Out缓冲区，所以response永远优先于out。
jsp中的html标签都是由转化成的out.write()输出的，如果用response输出那么可能会打乱布局
![[Pasted image 20240417141339.png]]



### EL表达式 
#### EL表达式的使用
##### 运算（算数，比较，逻辑，空）
![[Pasted image 20240417201734.png]]
![[Pasted image 20240417204758.png]]
##### 获取值
![[Pasted image 20240417201803.png]]
![[Pasted image 20240417204441.png]]
域名称对应于JSP中的内置对象，其域的范围从小到大是，
`pageContext<request<session<application`

###### 获取隐式对象
![[Pasted image 20240417205139.png]]


### JSTL
#### JSTL概念、使用步骤和常见标签
![[Pasted image 20240417213021.png]]
![[Pasted image 20240417213155.png]]

#### if标签
![[Pasted image 20240417213342.png]]
- 使用案例：
![[Pasted image 20240417213308.png]]

#### choose标签
![[Pasted image 20240417212144.png]]
#### foreach标签（最重要最常用）
##### 导入
循环常用于完成重复操作和遍历容器，现在就是如何使用foreach标签分别实现这两个功能
![[Pasted image 20240417213511.png]]
##### 实现完成重复操作
![[Pasted image 20240417213701.png]]
**使用案例：** 遍历1到10
`<c:forEach begin="1" end="10" var="i" step="2">${i}</c:forEach>`
**分析**：
var="i" 相当于 int i
begin="1" 相当于 int i=1
end="10" 相当于 i<=10
step="1" 相当于 i++
并且其中的i是通过EL表达式进行访问的
##### 完成遍历操作
![[Pasted image 20240417214633.png]]
![[Pasted image 20240417214618.png]]

### Filter过滤器


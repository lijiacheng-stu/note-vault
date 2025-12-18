### web相关概念和模型
![[Pasted image 20240414143827.png]]
![[Pasted image 20240414143325.png]]
### web服务器软件--tomcat
#### 服务器软件相关概念
![[Pasted image 20240414144746.png]]


#### tomcat使用
##### 安装、卸载和启动（访问）、关闭
![[Pasted image 20240415114121.png]]
![[Pasted image 20240415114023.png]]
![[Pasted image 20240415114220.png]]
##### 项目部署方式
![[Pasted image 20240414163229.png]]
对细节的补充：
对于方式二：项目的存放路径是精确到文件夹的。虚拟目录(应用程序上下文？)，可以认为就是这个文件夹。在windows中目录的符号是反斜杠`\` ，在浏览器是斜杠`/` 


对方法的评价与选择：
**对方式一** 
需要将项目整个copy在webapps目录下，可能赋值粘贴比较麻烦，也可能会导致很占据内容，当项目修改后，需要重新删除上线等问题。不推荐。
**对方式二**
尽管是地址访问的形式，当文档动态改变后，仍然能够动态的修改。但是要在conf\server.xml文件配置。下架的时候也要在server.xml中修改，这种操作很危险，所以好，但是不推荐
**对方式三**
保留了有点，也规避了缺点。热部署，当不要的时候直接_bak就行。
##### 动态项目和静态项目目录结构的差别
![[Pasted image 20240414170055.png]]

##### tomcat集成到idea，并将项目部署到服务器上
疑问：被部署的项目出现在tomcat的什么位置呢？
![[Pasted image 20240414170324.png]]
热部署：当更新resources后，执行更新部署的操作，就是热部署
![[Pasted image 20240415090416.png]]
### Servlet
#### 概念
![[Pasted image 20240415095323.png]]
#### 配置原理、快速入门与执行原理
**配置原理** 
用户要访问一个servlet，对于用户来讲servlet是一个url，对于服务器来说servler是一个放在包下的类，所以需要有一个映射关系。配置这中映射关系，就是servlet的配置。
![[Pasted image 20240415101521.png]]
在配置中，servlet元素只是相当于给报名重命名了一下，servlet-mapping起到了关键作用，实现了包名与url之间的映射
**快速入门** 
![[Pasted image 20240415100553.png]]
**Sevlet执行servi方法的执行原理**
解释名词
- 资源路径
![[Pasted image 20240415101948.png]]
在这个路径下的路径：比如资源路径是/demo-->则路径为/core_content/demo
- 原理
- 
![[Pasted image 20240415101657.png]]
![[Pasted image 20240415101601.png]]
所以说tomcat是一个容器，如果离开了这个容器就没有人给类创建对象，调用方法，所写的类就没有意义了。

#### Servlet生命周期
![[Pasted image 20240415103302.png]]
![[Pasted image 20240415103326.png]]



#### Servlet3.0的注解配置
![[Pasted image 20240415103852.png]]
例如：
![[Pasted image 20240415104111.png]]
#### IDEA与tocat的相关配置
![[Pasted image 20240415110509.png]]
- 运行已经部署的项目，查看log的第一条，这个位置就是这个项目配置文件所在的位置
![[Pasted image 20240415110617.png]]
- 对于这个项目的配置文件是完全独立的，可以通过idea图形化界面进行修改
使得不同的项目具有自己独特的配置情况
![[Pasted image 20240415110718.png]]

- 通过访问config /catalina/localhost下的配置文件，可以观察到真实被部署的文件的位置
![[Pasted image 20240415111223.png]]
发现就在项目的out目录下面。
- 具体项目的目录结构如下
![[Pasted image 20240415111312.png]]
- web-inf目录下的class文件夹，对应工作目录的src下的类

#### Servlet的体系结构
**体系结构**
![[Pasted image 20240415112012.png]]
**GenericServlet的由来**
直接继承Servlet，但只需要实现service方法时，会显得很乱。GenericServlet就是Servlet的空实现而已，相当于是适配器类。
**HttpServlet的由来**
屏蔽了'GET'和'POST'的处理逻辑，在HttpServlet中已经实现了Service方法，但是还差一点拼图，就是doGet和doPost方法
![[Pasted image 20240415112248.png]]
**HttpServlet的使用案例**
- 对于Servlet的实现类
![[Pasted image 20240415112751.png]]
- 对于提交表单的html页面
![[Pasted image 20240415112840.png]]

#### Servlet_urlpattern的配置
![[Pasted image 20240415113507.png]]
- 其中`*`是通配符的意思
### http
#### http的概念和特点
![[Pasted image 20240415203346.png]]
#### request对象和reponse对象的创建者和使用原理
![[Pasted image 20240415155529.png]]
![[Pasted image 20240415155557.png]]
#### request对象
##### 请求消息数据格式
###### **请求行**
![[Pasted image 20240415151210.png]]

###### **请求头** 
![[Pasted image 20240415154441.png]]
- 对请求头中Referer作用解析
	- 统计工作
	根据referer来统计多少人点击了这个网站，从而判断出投入广告哪儿个更有受益
	![[Pasted image 20240415154816.png]]
	- 防盗链
	![[Pasted image 20240415154704.png]]
	盗取超链接的人盗取了优酷的流量，其实盗取了其广告受益
###### **空行和就请求体（正文）** 
![[Pasted image 20240415154534.png]]
**样例**
![[Pasted image 20240415154554.png]]




##### request对象继承的体系结构
![[Pasted image 20240415160100.png]]
实现类是apache写的，可以下载源码进行解析
##### 功能
###### 功能1：获取请求信息数据，带星掌握*内容
 **获取请求行消息**
![[Pasted image 20240415161725.png]]
- URI 和URL 的区别：
![[Pasted image 20240415163217.png]]
**获取请求头数据**
![[Pasted image 20240415164257.png]]
**获取请求体数据**
![[Pasted image 20240415165137.png]]
- 例子：
![[Pasted image 20240415165605.png]]
![[Pasted image 20240415165615.png]]
![[Pasted image 20240415165628.png]]
![[Pasted image 20240415165649.png]]
###### 其他功能（对功能1的封装）
**获取请求参数通用方式**
请求参数就是指的就是form里面的键值对：username=zhangsan&password=ljc123
![[Pasted image 20240415171121.png]]
**请求转发与共享数据**
![[Pasted image 20240415172329.png]]
- 转发数据的模型
![[Pasted image 20240415212738.png]]

**获取ServletContext**
![[Pasted image 20240415174741.png]]




##### BeanUtils的使用
###### ppt中的介绍
![[Pasted image 20240418111109.png]]
注意：
属性名称和成员变量名称的差别：
- 属性名称是：setter或getter方法的名称去除set或get剩下的部分，再将首字母从大写改成小写
- 成员变量名称：就是`privite 数据类型 成员变量名称;` 这样修饰的部分
###### commons-beanutils-1.9.3-bin.zip版本的使用
声明：三大方法指的是以下三个方法
- getProperty() //property属性的意思
- setProperty()
- populate()
和视频中BeanUtils的使用区别：
- 三大方法定义在了BeanUtilsBean这个类中。
- 得创建对象才能引用了， 因为三大方法不是静态方法了。
方法的使用：
- 对于get或set方法
name参数，写属性名，将调用属性名的方法将设置的值设置过去或取出来
- 对于populate方法
每个键值对分别调用get和set方法，没有就是null，多了就报错
#### response对象
##### 响应消息数据格式
###### 相应行
![[Pasted image 20240415204445.png]]

- 302：重定向
![[Pasted image 20240415205128.png]]
解释：客户端向服务器发起资源A的请求，服务器接受并解析了请求，但是这个请求A解决不了，但是资源C可以解决,所以A告诉客户端去找C去吧
- 304 访问缓存
![[Pasted image 20240415205456.png]]
解释：浏览器访问完一次服务器后会在缓存中存储一些信息，比如a.png。当浏览器第二次向服务器请求已经缓存了的资源的时候，服务器能够解析到这个资源自己没有改变过，让浏览器直接访问自己的缓存。
###### 相应头，相应空行，响应体
![[Pasted image 20240415205011.png]]
**例如：**
![[Pasted image 20240415204533.png]]
##### Response功能
###### 设置相应消息的主干函数
![[Pasted image 20240415210351.png]]

注：这里面的是最主要的功能，还有对这些功能的封装在下面案例中体现
##### 路径：相对路径和绝对路径
![[Pasted image 20240415213414.png]]
对于是否需要加虚拟目录的原因的形象解释：
一班和二班都有叫张三的同学，一班的张三点了一份外卖，外卖小哥给张三送餐
- 不需要加虚拟目录的情况
![[Pasted image 20240415213601.png]]
外卖小哥跑到一班，只需要含“张三，你的外卖到了”，不需要喊“一班的张三，你的外卖到了”，因为外卖小哥在一班喊，默认就是一班的同学啊。
等价于
当一个服务器内的资源跳转的绝对路径不需要加虚拟目录，因为在服务器内，资源默认就是在虚拟目录下的。
- 需要加虚拟目录的情况
![[Pasted image 20240415214135.png]]
外卖小哥在过道必须得含“一班的张三，你的外卖到了”，而不能只喊“张三，你的外卖到了”，因为不能确定是哪儿个班的张三，众多张三会产生歧义。



##### 案例
###### 案例1：完成重定向
![[Pasted image 20240415211653.png]]

###### 案例2：输出字节数据
### 会话技术
#### 概念与快速入门
![[Pasted image 20240416093339.png]]
![[Pasted image 20240416093823.png]]
注：Cookie和Session最主要的区别是共享数据存储的位置。Cookie存储在客户端浏览器，Session存储在服务器端。
#### Cookie
##### 概念、快速入门与原理
![[Pasted image 20240416093216.png]]

![[Pasted image 20240416093138.png]]
- 第一次响应请求中：
客户端发起了请求，这个请求对应访问的资源是CookieDemo1这个Servlet，执行sevice代码后，服务器回送了响应消息，响应消息中含有一个响应头set-cookie。
- 第二次响应请求中
客户端浏览器自动得将set-cookie中得数据，放在请求头cookie中，包装在请求数据中（只要服务器是与第一次是同一个），CookieDemo2将能收到并能解析Cookie




##### 细节
![[Pasted image 20240416173638.png]]
![[Pasted image 20240416173706.png]]
注意:
存储在客户端的cookie回来发送request请求的时候把cookie发出去（至于服务器对cookie是否解析，这个是浏览器管不着的），细节四就是指明在哪儿写情况下会将cookie发送出去。
##### 特点与作用
![[Pasted image 20240416173318.png]]
特点到作用的逻辑转换：
- 由于Cookie存储在客户端浏览器，所以数据不安全，容易被篡改，所以cookie用来存储不敏感的数据
- 由于浏览器对单个Cookie的大小，以及单个域名存储的cookie数量都有限制，所以只能存储少量数据
- 当浏览器长久存储了某个域名的cookie后，当再次访问时，发送请求时会将cookie发送给对应服务器，服务器通过解析得知了这个浏览器进行了哪儿写设置啥的。
#### Session
##### session对象的获取与使用
![[Pasted image 20240417142820.png]]
##### session的原理
 当servlet要获取session对象，但检测到request中没有JSESSIONID的时候，服务器会开辟一个Session的内存空间，用JSESSIONID来标识。此时servlet可以向session中添加和获取数据。 结束后，JSESSIONID的信息会自动地以cookie的形式发送给浏览器。 根据cookie的原理，在这次会话中的每一次请求都会携带含有JESSIONID的cookie给服务器。服务器就能根据JSSEIONID找到Session存储在服务器中的位置而不会再创建session
![[Pasted image 20240417143024.png]]
##### 原理的细节与问题补充
- **服务器未关闭，但是客户端关闭了，再访问该资源，两次获取的session是同一个吗？**
答：不是。根据cookie的原理，但关闭服务器后，默认cookie会释放，那么下一次访问后，请求消息将不携带JSESSIONID信息，服务器又将重新创建新的session
- **客户端不关闭，服务器关闭后，两次获取的session是同一个吗？**
答：不是，但是数据不丢失。
假设服务器已经有session，则客户端的Cookie中必然后JSSESSIONID。根据Cookie的原理当服务器关闭后，但服务器不关闭，那么客户端Cookie不受影响，下次访问服务器request仍然会将携带有JSESSION的Cookie发送给服务器。
服务器关闭前，会将Session中的信息序列化到硬盘上，称为session的钝化。服务器启动后，会将session文件加载回内存中，称为session的活化。活化之后，与钝化前session的存储空间已经不同了，所以说不是同一个，但是里面存储的数据是相同的，而且也能用JSESSIONid找到文件的新的在内存的位置，所以数据不丢失。
![[Pasted image 20240417145039.png]]
- **Session的失效时间？**
![[Pasted image 20240417145412.png]]
设置失效时间的方法：tomcat-->config-->web.xml-->session-cofig标签-->设置session-timeout的时间，单位分钟。

##### session的特点
![[Pasted image 20240417145558.png]]




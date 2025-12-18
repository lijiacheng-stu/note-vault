### maven
#### 安装
官网下载->直接解压缩
配置环境变量：MAVEN_HOME 在Path中填%MAVEN_HOME%\bin
#### 仓库
##### 三类仓库以及它们之间的关系
- 三类仓库：
![[Pasted image 20240419101816.png]]
- 关系：
![[Pasted image 20240419102016.png]]
需要的jar包现在本地仓库找，没找到，则去中央仓库找；如果配置了远程仓库，先去本地仓库找，再去远程仓库找，最后再去中央仓库
##### 自定义本地仓库位置
- config->settings.xml中默认的repository的位置
![[Pasted image 20240419103552.png]]
- 我将本地仓库的文件夹命名为了mvn_repository，放在了maven的安装目录下
![[Pasted image 20240419104134.png]]
![[Pasted image 20240419104204.png]]
##### 自定义远程仓库位置
```
<mirror>
    <id>nexus-aliyun</id>
    <mirrorOf>central</mirrorOf>
    <name>Nexus aliyun</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```
	![[Pasted image 20240419104506.png]]
	
#### maven创建的项目的结构
![[Pasted image 20240419150426.png]]
注意：
- java目录相当于以前工程中的src目录
- webapp目录相当于以前web工程的web目录
```
--src
	--main
		--java
		--resources
		--webapp
			--WEB-INF
			--*.html
			--*.jsp
	--test
		--java
		--resources
```
	




#### maven中的常见命令
- compile
简言之：java文件编译成字节码文件，生成的文件放在target目录下
![[Pasted image 20240419151548.png]]
- clean
删除已经生成的target文件
- package
生成war包，添加到target文件中
- install
安装到本地仓库-->不是很理解

#### maven的生命周期
有三套生命周期，同一套生命周期，执行垢面的操作，会自动执行前面的操作
- 三套生命周期
![[Pasted image 20240419153247.png]]
![[Pasted image 20240419153519.png]]
##### maven的概念模型
![[Pasted image 20240419152848.png]]
分成上下两部分：
- 上半部分依赖管理
jar包: local -->b2b-->central,最后下载到本地仓库中
- 下半部分生命周期的管理
每个生命周期的完成依赖于一些插件，这些插件也放在本地仓库中。这也解释了为什么在没有导入jar包的时候也要安装那么多东西，其实就是插件。

#### maven坐标
##### 格式
![[Pasted image 20240419153802.png]]
##### 应用的位置：pom.xml文件
对本项目的goupId actifactID version进行定义
![[Pasted image 20240419154058.png]]依赖包
插件
	![[Pasted image 20240419153920.png]]
##### 作用原理
对于插件和依赖jar包就是向仓库中找，找不着再从私服和central中找来下载

#### IDEA中对maven的使用
##### 在IDEA中配置maven环境
![[Pasted image 20240419105849.png]]
##### 标签的体的作用与种类
###### 标签
- `<packaging></packaging>`
![[Pasted image 20240419154748.png]]
###### 标签结构
**依赖的结构**
- 依赖的结构
dependencies中包含多个dependency，
dependency中有四个标签，坐标(三个)+依赖范围
```
<dependencies>  
  <!-- https://mvnrepository.com/artifact/junit/junit -->  
  <dependency>  
    <groupId>junit</groupId>  
    <artifactId>junit</artifactId>  
    <version>4.13.2</version>  
    <scope>test</scope>  
  </dependency>  
</dependencies>
```
 - 插件的结构
 build中有plugins标签，标签中有多个plugin
 每个plugin有坐标+configuration（每种插件不同）
 ![[Pasted image 20240419162312.png]]

##### 执行maven的生命周期有关的命令
方式一：通过侧边栏的Maven图标进行执行
![[Pasted image 20240419155654.png]]
方式二：将高频的maven命令进行封装
![[Pasted image 20240419155943.png]]
##### 导入jar包或插件
###### 方法一：访问网站知道导入的名称与格式
[Maven Repository: Search/Browse/Explore (mvnrepository.com)](https://mvnrepository.com/)



###### 方法二：使用idea中的默认模板
alt+insert
![[Pasted image 20240419162058.png]]

##### 运行web项目
###### 方式一：传统方式
- Edit Comfigration->+Tomcat Server->Deployment
- 导入依赖
![[Pasted image 20240419165702.png]]

###### 方式二：使用插件
注意：使用插件时，servlet的依赖一定要加scope标签，否则报错
![[Pasted image 20240419171256.png]]
- 打开pom.xml，加入以下
```
 <!--    tomcat 插件-->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
        <configuration>
          <port>80</port>
          <path>/</path>
        </configuration>
      </plugin></plugins>
  </build>
```
- 观察maven中对应的插件
![[Pasted image 20240419171045.png]]
- 右键选择modify run configration 加入到run中
![[Pasted image 20240419171111.png]]

##### 依赖范围
含义：依赖范围指的是当前导入的dependency对哪儿些范围是有效的。
![[Pasted image 20240419172219.png]]
运行时环境，就是生成的war包中是否要加入依赖包。
![[Pasted image 20240419171439.png]]
- compile是默认值
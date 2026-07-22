- data persistence 数据持久化
- aggregate 聚合
- umbrella project 总项目；项目家族
- domain model 领域模型
- Entity 实体  （和table的含义是等价的）
- record 记录
- Cardinality 基数
- Business objects 业务对象
- DDL = data definition language 
-  cumbersome 繁琐的
- formula 公式；配方 (复数, formulas，formulae `/ˈfɔːmjʊliː/`)


新认识(碎片)：
- save方法之所以要返回存储的对象，是因为对象有部分信息只有在save执行后，才知道。例如，placed_at， id。
- 类图（Class Diagram）和数据库 Schema 设计之间存在一个转换过程，叫做 Object-Relational Mapping, ORM。
- ERD和类图是不一样的！类图是构建和可视化面向对象的系统的图像符号；ERD是一种用于数据库设计的结构图。
- 在ERD中，要将“One-to-One”, "One-to-Many"和“Many-to-Many”的关系进行存储。对于"One-to-Many"，外键如果存储在one-side那么列就不定了，在many-side可以稳定是一列，因此，在many-side；对与“Many-to-Many”，从左往右看，一对多，左边不能存，从右往左看，一对多，右边不能存。因此需要一个连接表，分别连接两边。
- Object-Relational Mapping(ORM):


认识性问题：
- 数据库中其他类型的数据如何转化？
- Optional是什么数据类型
- `private void saveIngredientRefs(long tacoId, List<IngredientRef> ingredientRefs)` 声明和调用真的匹配上了吗·saveIngredientRefs(tacoId, taco.getIngredients());·
- implements Serializatable 啥意思？serialVersionUiD又是什么东西？
- 怎么无损实现curd，包裹ingredient_Ref的？
- implement `Persistable`？

## 发现
### 1. application context 的创建和spring boot的优势
- `SpringApplication.run(TacoCloudApplication.class, args)`  将创建一个application context
	- SpringApplication执行具体的创建过程
	- `TacoCloudApplication.class` 告诉它应该如何构建这个 ApplicationContext，`TacoCloudApplication.class`需要被`@SpringBootApplication`注解
- `@SpringBootApplication`
	- @SpringBootConfiguration: 说明`TacoCloudApplication.class`能作为配置类使用
	- @EnableAutoConfiguration：它会根据引入的依赖、配置文件和运行环境，推断出你大概率需要什么，并提前帮你把这些基础设施 Bean 配好。
	- @ComponentScan:  告诉了SpringApplication扫描的跟路径，并且让他基于这个根路径，查找@component这些注解生成对应的bean。
### 2. springboot现在的Initializr只有4.0版本以上，引入h2后，无法autoconfiguration出h2-console了，需要额外得引入依赖了
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-h2console</artifactId>
</dependency>
```
可能的原因：
1. h2-console的自动配置与h2的引入解偶了 （更愿意相信这个）
2. 存在兼容性问题


## 综合知识
### 1. Relationship between classes
- Inheritance 继承，` is a`
- association 关联
	- aggregation 聚合，`is part of`, 两者生命线独立 
	- composition 组合，`is part of`, Class2不能独立存在
	- Dependency 依赖
- Realization 实现

### 2. vp的功能探索
### Key Support Features
- **Bidirectional Synchronization**: You can automatically transform a Class Diagram into an ERD and vice versa. This ensures that changes in your object model are reflected in your data model, maintaining consistency throughout the development lifecycle.
- **Object-Relational Mapping (ORM)**: Visual Paradigm supports ORM, allowing you to map data models to object models. This facilitates the generation of executable persistence layers (like Hibernate) directly from your diagrams. 
- **Comprehensive ERD Tools**: The platform supports conceptual, logical, and physical data models. It includes features for database schema generation (DDL), SQL statement generation, and reverse engineering existing databases into ERDs.
- **AI-Powered Generation**: Modern versions include AI tools that can generate both Class Diagrams and ERDs from text descriptions or problem statements, speeding up the initial design phase.
- **Inheritance Strategy Support**: When synchronizing between models, the tool can handle different inheritance strategies (e.g., Table-per-Class, Table-per-Subclass), automatically creating or re-creating entities to respect the chosen strategy.



## 想法：
1. 用spring-boot-starter-jdbc实现对数据的处理

## 对想法1
从以下方式探索：
- 看一下vp是否能直接生成对应的代码，避免手动输入产生错误
- 看一下h2-console能否查看插入的表的信息
- 写增删改查的代码，理解ORM的细节
### 1.1 对vp的探索
可以直接生成各种指定的数据库的代码。不过需要进行一定的配置，从Database Configuration中配置默认的数据库。这个原因在于，vp需要知道生成的是哪儿个数据库的代码。此外，vp还能够执行生成的代码，所以配置的时候，还可以添加jdbc。vp甚至可以插入对应的数据，不过需要在vp阶段就手动写入样例数据。
所以vp对database操作的代码都会生成出来，用于自己的项目。
尝试在mac上安装mysql和前端，用于快速检验vp的能力
##### 对brew的探索
前置知识：
- 在Homebrew中，命令软件的包叫做formulae，GUI软件叫做casks。homebrew/cask和homebrew/core是Homebrew官方维护的包仓库，其他仓库叫做tap，可以配置。
- homebrew安装的所有软件通常会在`HOMEBREW_PREFIX: /opt/homebrew`中的子目录中，GUI是例外

使用场景：
1. 如何下载一个包(以mysql为例)
	- `brew search mysql` 查看是否有这个包
		- 可以观察到formulae和casks两栏内容，可以通过--cask给命令，用于显示指定。
	- `brew install mysql` 安装这个包
	- `brew list` 查看brew管理的包中是否存在mysql
	- `brew info mysql` 查看mysql的具体情况
2. 如何卸载一个包：
	- `brew uninstall mysql`
3. 如何更新brew，以及它所管理的包
	- `brew update`升级brew
	- `brew upgrade mysql` 升级指定包
	- `brew upgrade`升级所有包 
	- 注： 一个包升级到更新版本，其旧包仍然保留
4. 如何管理它管理包中的服务：
	- `brew services start mysql` 启动，注册为macos管理的后台服务
	- `brew services stop mysql` 关闭, 从注册的macos管理的后台服务中删除
5. 其他：
	- `brew config`: 查看代理配置之类
##### 环境配置
- 用brew安装dbeaver，这个mysql前端
- 用brew安装mysql，并用`brew services start mysql`启动服务
- 用dbeaver连接mysql，并创建tacocloud这个database
- 在vp中，也进行相应配置

##### 用vp中绘制的ERD，生成正确的表格，并插入样例数据
具体的过程`https://www.visual-paradigm.com/tutorials/sdevsgendb.jsp` 参考这个网址
### 1.2 对h2-console的探索
h2-console能够看h2数据库，我们发现，竟然是没办法用dbeaver连接h2数据库，得改成文件，不用内存模式才行。

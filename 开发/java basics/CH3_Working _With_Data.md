- data persistence 数据持久化
- aggregate 聚合
- umbrella project 总项目；项目家族
- domain model 领域模型
- Entity 实体  （和table的含义是等价的）
- record 记录
- Cardinality 基数
- Business objects 业务对象


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
- 看一下vp是否能直接生成对应的代码，避免手动输入产生错误
- 看一下h2-console能否查看插入的表的信息
- 写增删改查的代码，理解ORM的细节
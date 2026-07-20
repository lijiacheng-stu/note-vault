- data persistence 数据持久化
- aggregate 聚合
- umbrella project 总项目；项目家族
- domain model 领域模型
- Entity 实体  （和table的含义是等价的）
- record 记录
- Cardinality 基数
- Business objects 业务对象


新认识：
- save方法之所以要返回存储的对象，是因为对象有部分信息只有在save执行后，才知道。例如，placed_at， id。
- 类图（Class Diagram）和数据库 Schema 设计之间存在一个转换过程，叫做 Object-Relational Mapping, ORM。
- ERD和类图是不一样的！类图是构建和可视化面向对象的系统的图像符号；ERD是一种用于数据库设计的结构图。

问题：
- 数据库中其他类型的数据如何转化？
- Optional是什么数据类型
- `private void saveIngredientRefs(long tacoId, List<IngredientRef> ingredientRefs)` 声明和调用真的匹配上了吗·saveIngredientRefs(tacoId, taco.getIngredients());·
- implements Serializatable 啥意思？serialVersionUiD又是什么东西？
- 怎么无损实现curd，包裹ingredient_Ref的？
- implement `Persistable`？


## Relationship between classes
- Inheritance 继承，` is a`
- association 关联
	- aggregation 聚合，`is part of`, 两者生命线独立 
	- composition 组合，`is part of`, Class2不能独立存在
	- Dependency 依赖
- Realization 实现

## ERD
- 一种用于数据库设计的结构图
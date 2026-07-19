- data persistence 数据持久化
- aggregate 聚合
- umbrella project 总项目；项目家族

新认识：
- save方法之所以要返回存储的对象，是因为对象有部分信息只有在save执行后，才知道。例如，placed_at， id。
- 

问题：
- 数据库中其他类型的数据如何转化？
- Optional是什么数据类型
- `private void saveIngredientRefs(long tacoId, List<IngredientRef> ingredientRefs)` 声明和调用真的匹配上了吗·saveIngredientRefs(tacoId, taco.getIngredients());·

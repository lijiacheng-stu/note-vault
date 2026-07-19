- data persistence 数据持久化
- aggregate 聚合


新认识：
- save方法之所以要返回存储的对象，是因为对象有部分信息只有在save执行后，才知道。例如，placed_at， id。
- 

问题：
- 数据库中其他类型的数据如何转化？
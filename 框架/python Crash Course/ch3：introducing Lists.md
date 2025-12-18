1. 规范： 用复数的名称给列表命名，如：letters，digits，cats
2. 定义：`bicycles = ['trek', 'cannondale', 'redline', 'specialized']`
3. 查，改： 
	- 语法：`print(bicycles[0])` `print(bicycles[-1])`
	- 技巧：可以把`bicycles[0]` 看成变量
4. 增：
	- 语法：`motorcycles.append("append_brand")`
	`motorcycles.insert(1,"insert_brand")`
5. 删：
	- 语法：`del motorcycles[0]`
	`popped_motorcycle = motorcycles.pop()`
	`popped_motorcycle = motorcycles.pop(1)`
	`motorcycles.remove('trek')`

6. 排序：
```
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort(reverse = True)
sorted(cars)
cars.reverse()
```
7. 长度 `len(cars)`
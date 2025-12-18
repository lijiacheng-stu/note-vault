一、 循环与list
1. 使用循环的意义：
通过不使用循环的麻烦来体现。For one, it would be repetitive to do this with a long list of names. Also, we’d have to change our code each time the list’s length changed.

2. 语法：
- 结构：
```
magicians = ['david', 'lily', 'calina']
for magician in magicians: 
	print(magician)
```
- 适用数据类型：
	- list   -> `players[:3]`
	- range()

3. 0逻辑错误的含义：
 This is a logical error. The syntax is valid Python code, but the code does not produce the desired result because a problem occurs in its logic.

4. 通过循环，向list中追加数字
```
//普通方式
squares = []
for value in range(1,11):
	squares.append(value ** 2)

//List Comprehension方式
squares = [value ** 2 for value in range(11)]
```

二、part of lists
5. Slices
6. copy a list
```
//正确，深拷贝
my_foods = ['pizza', 'falafel', 'carrot cake']
friend_foods = my_foods[:]

//错误，浅拷贝，指向相同的列表
my_foods = ['pizza', 'falafel', 'carrot cake']
friend_foods = my_foods
```
三、tuples
7. 特性：an immutable list is called a tuple.
8. 定义：
```
foods = 'vagetable','fruite','watermelon'
//加上括号起到装饰作用
foods = ('vagetable','fruite','watermelon'）
//单元素元组,注意有个逗号
foods = 'vegetable',
```
9. 技巧：尽管变量label那tuple不能修改数据，但是变量可以label其他的数据，通过这样来改变。
```
dimensions = (40, 50)
dimensions = (70, 80)
```

四、传值？传地址？
10. 传地址: 
list传的是地址，而不是值。 
因此：
- 函数中对list的修改是永久的
- 将list变量互传，对其中一个变量修改list，其他变量访问时，也修改

10. 传值：
```
var = list_name[:]
```
除非有特殊原因，否则应该传地址，因为传地址的方式更加高效。而传值的话，需要额外的时间和空间去传。
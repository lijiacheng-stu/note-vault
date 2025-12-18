一、Data Stuctures amd Sequences
1. 元组：
能改对象本身地内容，但是元组存储地这个对象不能该。
```
个人解释：
// 元组本质上是一个不可边地数组， 数组地每个位置都是一个指针， 指向一个对象。元组中每个位置地指针是`* const p`是`const *p`

现象：
// While the objects stored in a tuple may be mutable themselves, once the tuple is  created it’s not possible to modify which object is stored in each slot
// If an object inside a tuple is mutable, such as a list, you can modify it in place

推论：
// tuple不一定是hashable的
```


2. Variable Unpacking 
- 在for循环中的unpacking
```
seq = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
for a, b, c in seq:
	print(f'a={a}, b={b}, c={c}')
```
- 仅仅需要开头，不需要结尾
```
values = 1, 2, 3, 4, 5
a, b, *_ = values
```
- 复杂的解析
```
tup = 4, 5, (6, 7)
a, b, (c, d) = tup
```

3. list
- list(): The list built-in function is frequently used in data processing as a way to materialize an iterator or generator expression
- a.sort()： 其中的key关键字用于输入排序的函数
- slice：切片，正负可以混着来，左开右闭，`[start:stop]`, 没有空格


4. dictionary
- Valid dictionary key types：scalar types (int, float, string) or tuples (all the objects in  the tuple need to be immutable, too) 等价于 可哈希。hash(Object) 有值


5. Built-in Sequence Functions
- enumerate()
- sorted()
- zip()
- reversed()

- sequence的数据结构：
	- tuple
	- list
	- string
	- range

6. List，Set， and dictionary comprehensions
- 可嵌套
- list:
![[Pasted image 20250614164804.png]]
- set:
![[Pasted image 20250614164825.png]]
- dictionary:
![[Pasted image 20250614164842.png]]

7. 思维
差不多的东西，是可以进行转化的，直觉法。例如：
```
//例1
dict(zip(range(1,4),range(7,10)))
Out[8]: {1: 7, 2: 8, 3: 9}

//例2
dict(enumerate(range(5)))
Out[11]: {0: 0, 1: 1, 2: 2, 3: 3, 4: 4}

// 例3
list("hello world")
Out[9]: ['h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd']
```


二、Functions
1. 语法糖：`stu.eat()` 等价于`Student.eat(stu) `
2. fuction是（callable的）对象,所以具有一般函数的性质，也具备callable的性质：
	- 函数名是函数对象的引用，是可以改的。
	- 可调用，所以后面可以加`()` 用于函数调用
3. `map()` 函数可以作为少了条件筛选的list comprehension的替代品，因为执行的操作是一样的，返回值也是列表。
4. 当函数有函数对象作为参数时，常用lambda function（匿名函数）作为这个参数
5. generator和iterator的关系：generator是特殊的iterator。iterator通过`__next__()`来获得下一个对象的。
	- generator的函数创建法：generator的定义时用yield而不是return，每次执行并返回一个yield。
	- generator的Generator expressions创建法： To create one, enclose what  would otherwise be a list comprehension within parentheses instead of brackets
	- Generator expressions创建法的用途：Generator expressions can be used instead of list comprehensions as function arguments in some cases
6. Errors and Exception Handing：
	 - try：里面写可能出现异常的代码，下面三个代码块怎么执行取决于try的执行情况
	 - except：指定异常情况，什么都不写，那就是任何情况都这样处理。可以写元组。
	 - else： 当try成功时执行
	 - finally： 无论try成功与否，一定执行
```
f = open(path, mode="w")

try:
    write_to_file(f)     # 尝试写入文件
except:
    print("Failed")       # 如果出错，打印失败信息
else:
    print("Succeeded")    # 如果没有出错，打印成功信息
finally:
    f.close()             # 无论是否出错，都要关闭文件
```

三、Files and the Operating System
1. file的打开和关闭，用with语句就不用关心关闭了
2. 

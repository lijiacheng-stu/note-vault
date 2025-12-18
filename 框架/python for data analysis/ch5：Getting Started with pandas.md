#### 一、介绍
1. 与pandas一起配合使用的工具：
	- 数值计算工具：NumPy，SciPy
	- 分析库：statsmodels，scikit-learn
	- 数据可视化库：matplotlib
2. pandas与numpy的关系：
	- 同：pandas采用了很多numpy的编程惯用手法
	- 异：pandas处理表格和异类数据（如：每一列数据类型不同）,numpy处理同类型的数值数据

### 二、Series
1. series 的构成：
	- 一串值：a sequence of values (of  similar types to NumPy types) of the same type
	- 索引：an associated array of data labels,  called its index
```
// index由多个label组成
index:=['a', 'b', 'c']

//label是给每个数据点（元素）取的“名字”。
label:= 'a'
```
iloc的意义：
**还有一个 `iloc` 运算符，它专门使用整数进行索引，**  
**以便在索引是否包含整数时都能保持一致的行为。**




用途>框架>单条知识？


提到PandasArray是Array的封装，下面这个句子意味着什么？

The result of the .array attribute is a PandasArray which usually wraps a NumPy  array but can also contain special extension array types

1. pandas中`obj2[["c", "a", "d"]]` 这里的操作类似于fancy indexing，所以怎么称呼这样的做法？



2. 在series中能否有label based 和 integer based indexing?
3. Interpolation (fill) method?`
4. `In [111]: frame.reindex(states, axis="columns") ` 这里的axis能否使用0 1

5. `The row selection syntax data[:2] is provided as a convenience. Passing a single  element or a list to the [] operator selects columns.` 为啥第一个参数有的时候就是选行有的时候就是选择列呢?

6. Both indexing functions work with slices in addition to single labels or lists of labels 什么意思？

7. 可以放`[]` 里面是具体的labels， 也可以放单个label，slice，boolean array


三、indexing Selection and filtering
1. 回顾对numpy的索引:
	- 类型: basic index，slice，boolean indexing， fancy indexing。 
	- 形式:`arr[]` 

2. 关键问题：为什么要区分`.iloc`和`.loc` ，不能只是用`[]`?
	答：`ser[2]` 如果索引是数字，则会解析为label，如果索引是字母，则会解析为position。如:对于index为integer的情形, `ser[-1]`中`-1`看成label,没有这个label就会报错. 
	也就是说`ser[2]` 会因为index的类型而返回不同的结果。为了保持一致性，就在保持`'[]`的模糊性的基础上，清晰的分离出iloc和loc

3. 对于Series的索引方式：
	方式一：与numpy完全相同的方式 `arr.iloc[]` ,但是boolean array得是numpy类型或者list才行
	方式二：使用index进行索引`arr.loc[]` 或`arr[]` ，使用的是label来索引，仍然可以用numpy中的四种方式，此时boolean array可以是Series numpy和list型。

4. 对于DataFrame的索引方式:
个人:`[]`比较模糊,特殊情况多,还是得用iloc和loc
![[Pasted image 20250617233245.png]]
对以下异常的理解:
- 问题:![[Pasted image 20250617234626.png]]
- 分析:
	`data.loc[data.three == 5]["three"]` 是两个步骤的.步骤一`data.loc[data.three == 5]` 获得一个copy版本, 步骤二是对copy版本进行`["three"]`的索引.如果`data.loc[data.three == 5]` 则是copy的版本进行了赋值.
- 结论
	常用在赋值操作时要避免链式索引（chained indexing)

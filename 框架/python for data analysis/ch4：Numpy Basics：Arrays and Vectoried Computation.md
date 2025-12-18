#### 一、简介
1. numpy的特点：
	- 我不做高级菜，但我提供炉灶和食材。（但是面向用户的话，还是更常用基于numpy的pandas）
	```
	NumPy by itself does not provide modeling or scientific functionality
	
	NumPy provides a computational foundation for general numerical data  processing
	```
	 -  NumPy 提供了一个完整且文档齐全的 C 语言接口（C API），它使得 Python 和低级语言（如 C、C++、Fortran）之间的数据交互变得简单和高效
	
2. numpy为啥这么重要——高效：
	- python中的list存储数据时，存储的是对象的引用名，每个引用名指向的真正数据是离散的。而numpy存储数据就是存储统一类型数据，将数据对象直接连续存储。所以类型只需要在数组层面指定一次，不存在引用的情况，这样每个对象减少了存储型、引用计数这样的额外开销。（减少存储数据的内存开销，类型确认开销）
	- 计算是并行计算，而不需要通过循环计算每个元素。（减少了执行开销）
	- 这种内存有可以用C/C++这种高效的语言处理，减少高级语言的解释时间。（减少了常规解释python代码的开销）
3. 学习方法：
```
While it’s not necessary to  have a deep understanding of NumPy for many data analytical applications, becoming proficient in array-oriented programming and thinking is a key step along the  way to becoming a scientific Python guru.
```
4. 小结
- 对array的基础进行学习：包括创建（内存结构，各种数据类型，形状，list转化等等），索引（基本的索引和切片，布尔索引，花式索引），转置
- 对array的每个元素同时进行相同操作的函数
- 对array的整体进行操作：
	- 将条件逻辑表达为array操作
	- 数字 -> 数学统计
	- 布尔 -> 对布尔数组操作的方法
	- 排序
	- 集合方法
- 线性代数的操作
- 存取数组
- 其他：
	- 随机数生成器。（随机数生成器 + 随机分布 + 形状）生成一个数组
#### 二、对ndarray的基操
1. Creating ndarrays
1.1 array的属性：
- dtype
- ndim
- shape
1.2 创建方法
![[Pasted image 20250615110939.png]]

1. Basic Indexing and Slicing
1.1 重要性质：
- 对array的切片，本质上是原array的视图不是副本，所以对切片的操作会反映到原array上。这是由其处理大array的用途决定的。可以用`.copy()`来生成副本。
- `arr[0][2]` 和`arr[0,2]` 是相同的。但是个人认为是两种理解方式，第一种是`a[0]`的到的结果在arr1，在对arr1进行`arr1[2]`;第二种则是直接定位。`arr3d[1, 0]` 这种索引不适用有python中的list of lists
- Indexing with slices中用index会起到降低维度的作为，用等价的切片则不会出现降维。具体的细节： ![[Pasted image 20250615163031.png]]
- 当使用fancy index（花式索引）时，对花式索引直接赋值会改变原数组，将花式索引赋值给变量则是副本。同理，Boolean indexing也符合这个性质

#### 三、伪随机生成器
1. 用numpy的random模块生成随机数与用python中random模块生成随机数的区别：前者能够同时生成一块，后者只能一个一个生成
2. 生成随机数的方法：
- 旧API: np.random.standard_normal() 无随机种子，结合上下文生成随机数， 复现性能差
- 新API：
```
rng = np.random.default_rng(seed=12345)
data = rng.standard_normal((2, 3))
```
- 基于新API，生成其他分布的随机数
![[Pasted image 20250616013027.png]]
#### 四、universal functions：逐元素的数组函数
#### 五、Array-Oriented Programming with Arrays
通用：
- numpy的操作是效率更高的，但是只能用于对array
- numpy版本的方法是向量化的（对整个数组进行并行操作）所以更快，而且返回值也会是array类型而不是list类型
##### (一)Expressing Conditional logic as array operations

##### (二) Mathmatical and statistical methods
1. 统计方法的种类
![[Pasted image 20250616170458.png]]
2. 使用方法的分类
	- 可以对整个数据表进行统计
	- 可以分轴进行统计（如对列或对行求均值方差）
3. 方法的调用
	 - 通过array实例来调用方法`arr.sum(axis=1)`
	 - 通过numpy库中的函数调用`np.sum(arr,axis=1)`
4. 将上面的方法用于布尔数组时，True会强制转换成1，False会强制转换成0 

#### 六、矩阵运算
- `np.array([1,2,3,4])` 和 `np.array([[1,2,3,4]])`和`np.array([[1],[2],[3],[4]])`是不一样的

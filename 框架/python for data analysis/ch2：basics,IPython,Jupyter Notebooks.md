1. 引导部分：
- 库成熟了
- 介绍常用的内置数据结构和库
- 书中的大部分内容，集中于基于表的分析和数据准备工具
- 用IPython和Jupyter来探索工具

2. python的特性：
- 解释性语言：The Python interpreter runs a program by executing one statement at a time.

3. 运行python的方式：
- 文件：hello_world.py，然后`python hello_world.py`
- standard interacitive Python interpreter ：`python`
-  enhanced Python interpreter,`ipython` `%run filename`
- Jupyter notebooks `jupyter notebook`

4. IPthon的优势：
- 比print可好的可读性

5. tab completion:
- 开头字母，匹配合适的存在的方法和变量名（会隐藏`_` 开头的属性和方法，要查的话自己先输入`_`）
- 查点好后面对象相关的属性和方法名
- 函数中的输入参数

6. 自省introspection（`?`）：
- 查对象的性质
- 查方法的性质
- 结合通配符查模块中匹配的方法有哪儿些


7. python的更高理解：
- 一切皆对象：包括module。 Every number, string, data structure, function, class, module, and so on exists  in the Python interpreter in its own “box,” which is referred to as a Python object.

- 变量名是对Object的引用，是Object的名字，Object的类型存在Object中而不在名字上。

- Python 是一种强类型语言：在 Python 中，每个变量都有明确的数据类型，而且 **不会发生隐式类型转换**（或自动类型“强制转换”）——也就是说，**不同类型之间的操作必须明确转换，否则会报错**。

- 小细节：
	- python中的整除`//` ,求余`%` ,小数除`/`
	- `"""#多行字符串，换行会有不可见的换行符"""`
	- `s = r"this\has\no\special\characters"`
	- `f"{amount} {currency} is worth US${amount / rate:.2f}"`
	- 编码encode：将字符映射为01序列的过程； 解码：将01序列映射为字符的过程。 编码规则是函数`f`
	- None也是一个对象，整个Python中就一个None对象
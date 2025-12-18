一、Variable
规则与规范：
1. 区分好 rule 和 guideline：
	- rule：打破规则，则会报错
	- guideline：遵循规则，提高可读性
2. rule(个人需要):
	- 分隔单词不能空格，而是用下划线。
3. guideline：
	- 变量的命名用小写。大写另有用途

4. 对变量的理解：It’s much better to think of variables as labels that you can assign to values. You can also say that a variable references a certain value.

二、String
1. 定义：
A string is a series of characters.
2. 看成字符串的条件：单引号和双引号中都行
Anything inside quotes is considered a string in Python, and you can use single or double quotes around your strings
3. 改变大小写
4. whitespace
5. 单双引号的套用

三、Number
1. Integer
2. float
	- 产生任意小数的特殊情况：
	```
	0.2 + 0.1
	3 * 0.1
	``` 
	- 但凡float参与的运算，无论其结果是否为整数，结果默认都会是float类型
	-  除法，结果是整数也会是浮点数类型 
 3. underscores inNumbers
 ```
 universal_age = 14_000_000_000
```
 4. constants 
 无内置constant型，就将变量都大写

四、注释 comment （`#`）
五、Python之禅 The Zen of Python
1. 通过在terminal中输入以下获得。 它讲述的是写python代码的一些准则。
```
import this
```
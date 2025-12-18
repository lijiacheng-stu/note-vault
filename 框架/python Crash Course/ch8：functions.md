1. 函数的意义：
	- easier to write, read, test, and fix
	- 代码复用

2. 结构：
```
function definition:
	docstring
	body of the function

function call
```
样例：
![[Pasted image 20250609171300.png]]
3. parameter和argument
	3.1定义
		通俗地，函数定义地时候小括号中的变量叫做parameter，函数调用传入的值叫做argument
		![[Pasted image 20250609201723.png]]
	3.2 positional arguments (一种函数调用方式)
		argument的顺序和parameter的顺序要对应起来
	3.3 keyword aruguments (一种函数调用方式)
		传入参数的时候是键值对
		好处：不用担心传参的顺序问题
		细节：键值对之间没有空格
	3.4 default values
		对参数提供默认值，函数调用时可缺省，有默认值的参数必须写在右边。
		（因为在使用默认值的函数调用仍然可遵循positional arguments，如果默认放在第一，又使用默认参数，那函数调用的第一个给的是默认参数，而不是第二个参数了）
	3.5 用法： positional arguments和keyword arguments和default values可以混着来。
		![[Pasted image 20250609204508.png]]
	
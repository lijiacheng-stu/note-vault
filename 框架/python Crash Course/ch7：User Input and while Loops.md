1. 规范：
	 - 提示的末尾加空格 Add a space at the end of your prompts (after the colon in the preceding example) to separate the prompt from the user’s response and to make it clear to your user where to enter their text.
	
2. input：
	2.1 prompt的多行提示：创建prompt变量
![[Pasted image 20250609154651.png]]
	2.2 将input的的返回结果用int()，将数字的字符串表达形式转成数字表达形式
3. while循环：
	3.1 for循环和while循环的区别：
	```
	The for loop takes a collection of items and executes a block of code once for each item in the collection. In contrast, the while loop runs as long as, or while, a certain condition is true.
	```
	3.2  control the flow of a while loop：
	- 直接条件判断
	- flag: flag作为while的条件判断，多条件下对flag进行修改。
	- break / continue
	3.3 while循环对列表：
	- move items form one list to another
	- remove all instance of specific values form a list
	3.4 while循环对字典：
	- fill a dictionary with user input

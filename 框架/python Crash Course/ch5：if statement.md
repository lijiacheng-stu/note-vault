一、 条件判断 condition test 
1. conditional test: At the heart of every if statement is an expression that can be evaluated as True or False and is called a conditional test
2. 条件判断的本质：条件判断回答的问题是：当前状态符合某种条件对吗？
3. 一种编程思想：
	- 缘由：python在condition test时是对大小写敏感的，但是有时候需求是大小写不敏感的。
	- 做法：将变量转化成小写后比
	```
	car = 'Audi'
	car.lower() == 'audi'
	```
3. 布尔表达式 Boolean expression, 是condition test的别名
4. 对于空列表，if的条件判断中返回false，否则true

二、if statements 
1. else的一些糟糕的点：The else block is a catchall statement. It matches any condition that wasn’t matched by a specific if or elif test, and that can sometimes include invalid or even malicious data.
2. 一些结构：
---
![[Pasted image 20250528162445.png]]

---
![[Pasted image 20250528162614.png]]
---
![[Pasted image 20250528162505.png]]

---
![[Pasted image 20250528162635.png]]

---
3. if you want only one block of code to run, use an if-elifelse chain. If more than one block of code needs to run, use a series of independent if statements.

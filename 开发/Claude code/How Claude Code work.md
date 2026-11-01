## The Agentic Loop
![[Pasted image 20261101112158.png]]
- gather context
	- LLM：为完成任务，LLM决定收集哪儿些信息
	- 工具：收集
	- 我：
- take action
	-  LLM：为完成任务，结合收集的上下文信息，决定采取哪儿些行动
	- 工具：执行
	- 我：
-  verify results
	- 工具：运行 `mvn test`、编译项目、执行测试用例。
	- LLM：读取测试输出、分析报错、判断是否达到任务目标。
	- 我：

## Permission
You can choose how much oversight to keep while Claude works.
- plan mode：不能修改文件
- auto mode
- auto-accept：File edits and common filesystem commands like `mkdir`, `mv`, and `rm` are automatically approved, but other commands still require your permission.
- Manual
先使用 Plan Mode等 Claude 给出方案，你确认没有问题后，再切换到 Accept Edits 或 Auto，让它开始执行。

使用shift + tab切换mode
盲区：
- install the Claude in Chrome extension so Claude Code can control a browser tab and test the UI directly.
-  **subagent code reviewer**
- **  Include a test suite.**


- 第一步explore 和plan：在plan mode下进行explore和plan，这样做有两个好处，一是在修改前完成方向的就成，二是形成的如何得到结果的上下文，能够在后续code阶段指导Claude的下一步决策。
- 第二步code： 选择mannul，auto-accept，或者auto mode
- 第三步commit：在commit前，生成一个code reviewer subagent看一下代码，它不会携带主代理的偏见。
一、Introduction to ARM Based Processors:
1. arm的含义:
	- 一种精简指令集
	- cpu的一种完备的内核
2. 对基于ARM的处理器的理解ARM based processors：
	- ARM architecture revisions（个人简称，架构）：一种说明文档，定义了这中结构的芯片在各个维度上是怎样的（是一种标准）。如：ARMv6, ATMv6-M, ARMv7-M, ARMv7-A, ARMv8-M and so on 。（应该怎样？）
	- core architectures（简称，内核）：基于ARM achitecture实现的设计图纸或物理的处理器核心。实现后的芯片的命名和任意的，只有得到arm授权的公司才能够实现芯片的生产。其中，cortex-M是arm公司的制作的，用于授权给别人能直接用的成品。
	- 推论：有很多公司要么基于arm架构自己设计内核自己用，要么直接使用arm设计好的内核拿过来用。（怎样实现？）
3. ARM Holdings：是一家由日本软银控制的法国公司。不生产芯片也不售卖芯片，而是授权上述的架构和内核。
4. ST microelectronics（意法半导体）：
	- 是一家意大利和法国合资背景的企业，是被ARM Holding授权的企业之一，是直接使用arm设计好内核，设计自己处理器的半导体企业
5. cortex分为cortex-A , cortex-M, cortex-R。（ application，embedded，real-time）
	
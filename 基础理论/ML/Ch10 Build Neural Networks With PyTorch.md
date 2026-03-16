## 单词
- at scale 大规模地；在较大规模上；
2. 专业
	- in-place operation 原地操作
	- out-of-place operation 非原地操作



## Pytorch
- 基础：（tensor特有，或与numpy array不一样的地方）
	- tensor的创建
	- tensor和ndarray之间的转化
	- 原地操作 和 非原地操作
		- 原地操作的优势：save memory and speed up your models a bit by avoiding unnecessary copy operations,
	- pytorch对浮点数的默认精度及其理由
- 硬件加速：
	- 判断是否能获得硬件加速
	- 载入加速硬件；查看tensor所处的硬件
- autograd：
	- 声明叶子节点与
	- 前向传播
	- 反向传播
	- 在反向传播后，获取叶子节点的梯度
	- 梯度跟踪:
		- 节点更像“知道前驱，不知道后继”
		- 只要某个运算的输入中，至少有一个 tensor 需要梯度（`requires_grad=True`），并且当前不在 `torch.no_grad()` / `inference_mode()` 中，那么 PyTorch 通常会为这个运算构建计算图，并使输出也可追踪。
		- PyTorch 只在“原地操作可能破坏 autograd 正确性”时禁止它。  尤其是：**叶子节点（`requires_grad=True`）通常禁止原地操作**；非叶子节点是否允许，要看该操作是否会破坏反向传播所需的值。
		- 被自动跟踪的操作节点，根据计算图的依赖性质，可能无法原地修改输出，或输入，或两者都不能，或都能
	- 细节：
		- 梯度是累加的。有的是否要清除梯度
			- x.grad数据类型也是tensor
		- 为什么要使用with torch.no_grad(): 
			- 关闭梯度跟踪。解除对叶子节点的操作限制。
## 关键点
- gradient tracking
	- PyTorch will automatically keep track of all operations involving `x`：this is needed because PyTorch must capture the computation graph in order to run backprop on it and obtain the derivative of `f` with regard to `x`. In this computation graph, the tensor `x` is a _leaf node_.

ru
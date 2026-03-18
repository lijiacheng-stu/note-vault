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

h没有被依赖，因此，h += 1 后，f.backward()成功。
g被cos依赖，因此，g +=1后， f.backward()失败。
f被exp依赖，因此， f +=1后, f.backward()失败。


- mac上下载pytorch
	- uv add torch
		- : If you have a MacBook with MPS support ([Metal Performance Shaders](https://developer.apple.com/documentation/metalperformanceshaders)) then you don't need to upgrade the PyTorch libraries, as the default versions support MPS out of the box.
	- uv add numpy
- 对pytorch的底层，再进行归纳总结
	- 
- 对ch10阅读结束
- 阅读大预言模型ch2
- 寻找合适的图文检索的文章


# Pytorch底层归纳
## 术语
- leaf tensor
- no-leaf tensor
- backward function node
- AccumulateGrad node
- in-place operation: 变量名指向一个对象。非原地操作，操作会产生新的对象，让变量名指向新的对象。而原地操作，操作不对产生新的操作，变量名仍然指向原对象。
## 反向传播中，一个节点的任务
- f对当前节点的梯度已知
	- 反向传播过程中，有其计算图中的下游节点求得。
- 当前节点的输入节点的值已知道
	- 在前向传播时求到的
- 任务：需要求该点对其输入节点的偏导数
	- 将其输入节点按照该节点对应的符号组织在一起，然后求偏导
	- 根据偏导结果自然知道该节点的上下文依赖
		- exp：输出
		- cos：输入
		- mul：输入 
## autogrid是什么
### 定义
PyTorch comes with an efficient implementation of reverse-mode auto-differentiation  called _autograd_
### 做了什么呢？
从动态的角度来讲：
- 跟踪requires_grad属性为True的张量所参与的所有操作。存在新的操作，则在计算图生成新的node
- 新的操作带来前向传播，在前向传播过程中，对新的node添加必要的在反向传播计算梯度时所需的依赖的上下文信息，存储在`_save_*`属性中。这个上下文信息总是指向张量对象，以及存储该张量在此前向传播过程中的版本信息，防止反向传播过程中，因为张量被篡改导致错误。tensor的_version存储了版本信息。
	- `_version`是0，每修改一次自增1
	- 记录上下文信息，而不是放置node在前向传播中的值，是为了避免不必要的计算和复制。
从静态的角度来讲：
- 对于tensor变量，通过x.grad_fn得到tensor变量所绑定的计算图节点
- 计算图节点的next_functions属性，可以知道这个节点的输入节点
- 通过dir(计算图节点),获得`_save_*`属性，从而只有需要用于梯度计算的张量信息。总是尽可能指向已有的变量对应对象的内存,若没有，也会内部生成。
	- `_save_result`:记录该计算节点的输出值所对应的张量
	- `_save_self`：记录该计算节点的输入值所对应的张量
- 显示声明requires_grad属性的变量，指向AcumulateGrad node。由于需要从AcumulateGrad node中提取梯度，因此，必须有变量指向该node。当x += 1这类自增操作出现时，autograd会生成backward function node，并让x指向该 节点，这导致AcumulateGrad node没有被指向，出现运行时错误。其中一个解决方案是关闭autograd，**不生成**backward function node，x仍然指向AcumulateGrad node，从而避免错误。这样的方法是`with torch.no_grad():`
	- x = x + 1会让AcumulateGrad node没有被指向
	- y = x 
	- x = x +1
- 显示声明requires_grad属性为True的变量x所指向的对象leaf tensor，会指向AcumulateGrad node。由于需要从AcumulateGrad node中提取梯度，因此，必须需要有leaf tensor对象指向该node。当x += 1这类自增操作出现时，x所指向的对象leaf tensor的存储的数值会+1，由于autograd，跟踪了x += 1，会生成AddBackward0，且leaf tensor会指向新生成的AddBackward0，导致AcumulateGrad node没有对象指它。怎么避免呢？在`with torch.no_grad():`中操作 x += 1。因为关闭了autograd，因此，不会生成AddBackward0，leaf tensor存储的数值实现+1，仍然指向AcumulateGrad node。x = x + 1为什么允许呢？x = x + 1是，生成新的tensor对象，x指向它。但是原leaf tensor仍然存在，指向AcumulateGrad node。

## torch.nn.Module有什么特别的？
- parameters() / named_parameters()
- forward()
- register_forward_hook()
- register_backward_hook()
- can be called just like a regular function.
- 
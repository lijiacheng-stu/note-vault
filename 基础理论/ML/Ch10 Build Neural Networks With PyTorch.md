## 单词
- at scale 大规模地；在较大规模上；


## 关键点
- gradient tracking
	- PyTorch will automatically keep track of all operations involving `x`：this is needed because PyTorch must capture the computation graph in order to run backprop on it and obtain the derivative of `f` with regard to `x`. In this computation graph, the tensor `x` is a _leaf node_.
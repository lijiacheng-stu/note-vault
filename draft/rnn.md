## 问题：
- 继承nn.Module之后，为什么一定要运行一遍`super().__init__()`
- 为啥要的window length 提到batch size的前面？
	- 在我看来batch中的每一个都是能够并行执行的，因此，batch size在window length之前是很好的，并行能是能每次处理一个batch size大小的一个time step
	- 当window length提到batch size之前，就不能并行执行了，执行串行执行，每次执行的batch size大小和之前一样尽管。
	- 因此，好像没有什么意义把window length 提到batch size的前面
- 训练的时候，我希望是滑动窗口的作为target，但是验证的时候，只希望保留最后一个。那么，时候存在model.train（）和model.valid（）
- rnn中当前状态和当前的输出是不是一定得相等？对于LSTM好像h和y是相等的，gru也是，用Linear作为memory cell也是
## task：
- 手搓basic cell
- 手搓LSTM cell
	- 默认是处理batch的。对于输入的是非batch，则用unsqueeze转成batch，然后维持接下来的流程，最后在输出的时候还原，期间用is_batch做标记
	- 处理数据存在的默认输入问题，在函数签名中用None，在函数体里面根据形参是否为None来初始化默认的参数
	-  模块进入GPU，说的是模块的子模块或者属性进入GPU，可以通过初始化的device属性来手动配置，也可以to方法。但是对于forward是否能统一，to方法管不了，正确做法是在forward中创建的tensor的device和X的device相同。
- 手搓GRU cell
	- 图纸-->子模块名称
- 把cell组织起来，成为一个RNN层

- 获取hand-one machine learning中关于本章的样例数据
- 复现本章

## 基础知识：
### 1. 术语和参数
- batch size 
- window length 

- dimensionality --> input_size
- hidden size -->  hidden_size
- number of layers --> num_layers

- batch_first
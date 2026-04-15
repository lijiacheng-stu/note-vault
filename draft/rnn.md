## 问题：
- 为啥要的window length 提到batch size的前面？
	- 在我看来batch中的每一个都是能够并行执行的，因此，batch size在window length之前是很好的，并行能是能每次处理一个batch size大小的一个time step
	- 当window length提到batch size之前，就不能并行执行了，执行串行执行，每次执行的batch size大小和之前一样尽管。
	- 因此，好像没有什么意义把window length 提到batch size的前面
- 训练的时候，我希望是滑动窗口的作为target，但是验证的时候，只希望保留最后一个。那么，时候存在model.train（）和model.valid（）
- rnn中当前状态和当前的输出是不是一定得相等？对于LSTM好像h和y是相等的，gru也是，用Linear作为memory cell也是
## task：
- 手搓basic cell
- 手搓LSTM cell
- 手搓GRU cell
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
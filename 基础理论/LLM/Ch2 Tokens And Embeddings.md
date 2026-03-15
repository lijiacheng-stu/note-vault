## 一、LLM Tokenization
1. There are three major factors that dictate how a tokenizer breaks down an input prompt.
	- tokenization method
		- method1: byte paire encoding, BPE, used by GPT
		- method2: Word Piece, used by BERT
		- aim：optimize an efficient set of tokens to represent a text dataset
	- make a number of tokenizer design choices
		- example1: vocabulary size
		- example2: what special tokens to use
	- tokenizer need to be trained on a specific datasets to establish the best vocabulary it can use to represent that dataset.
		- code dataset
		- multilingual text dataset
		- English text dataset

看这段代码：

import torch

x = torch.tensor(6.3, requires_grad=True)
x += 1 # 报错，不理解。现在没有任何计算图，想自增长， 报错，RuntimeError: Trying to backward through the graph a second time


f = x ** 2 # 实现前向传播

x += 1 # 记为(1)，和预期一样，报错

f.backward() # 跳过(1)执行，实现反向传播。

f.backward() # 记为(2), 报错，RuntimeError: Trying to backward through the graph a second time

x += 1 # 记为(3)， 跳过(2)执行，和预期不一样，报错。

这个逻辑是奇怪的。(2)说明一次前向传播，只能执行一次反向传播，计算图就应该没有意义，可以释放了吧
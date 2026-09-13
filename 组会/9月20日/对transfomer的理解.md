1. 组建的层级关系
	- transformer
		- input embedding + positional encoding
		- encoder
			- encoder layer * N
				- multi-head (self-)attention
					- Q/K/V projection matrix (注意是三个矩阵)
					- attention heads （=scaled dot-product attention layer， 本身没有parameter）
					- output project matrix
				- Add & Norm (residual connection + LayerNorm)
				- feed forward network
				- Add & Norm 
		- output embedding + positional encoding
		- decoder
			- decoder layer * N
				- masked multi-head (self-)attention
				- Add & Norm 
				- multi-head (cross-)attention
				- Add & Norm 
				- feed forward network
				- Add & Norm 
		- language modeling head
			- 全连接层 （将decoder最后一层输出的hidden state，线性投影到词表空间的，得到vocab_size 维的logits向量）
			- softmax 函数 （可选）
2.  multi-head attention
	- 步骤：QKV Projection → Split into Heads →calculate Attention per Head → Concat → Output Projection
	- calculate Attention per Head ： scaled dot-product attention
		- ![[Pasted image 20260913175159.png]]
3. （scaled）Attention Score Matrix / Attention Scores
	- ![[Pasted image 20260913175047.png]]
	- 没有缩放：raw attention scores
4. Attention Weight Matrix / Attention Weights
	- ![[Pasted image 20260913175100.png]]
5. 对掩码的理解
	- 形式上：Mask 是作用在 Attention Score Matrix 上，把不允许关注的位置设为 −∞。（作用在放缩后的注意力分数上）
	- 本质上：对于每一个 Query，规定它“允许看哪些 Key”。
	- 两种常用场景：
		- Padding mask: ignore padding key
		- causal mask: ignore future key
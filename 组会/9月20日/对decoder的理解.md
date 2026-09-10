1. 对掩码自注意力力的理解
	- 输入的是token embeddings，输出的是contextual embeddings
	- 第i个token只能通过使用前i个token（包括第i个）的信息获得该token地contextual embedding
	- 本质上仍然是对句子中每一个token对应含义进行建模，区别在于因果的。（掩码自注意力仍然是在为每个 token 计算一个融合上下文信息的表示，只不过这种上下文信息受到因果掩码的限制。）这里的因果的指的是自回归的过程中，要求能够通过第i个token的上下文嵌入推理第i+1的token，第i个token只能知道第1～i个token的信息，所以第i个token地上下文嵌入也只能利用第1～i个token的信息。
2. 对KV Cache的理解
	- 推理阶段，对于第i个token地上下文嵌入，不会随着新token的加入而发生改变，继而基于此上下文嵌入得到的对vocabulary length大的概率向量也是不变的。
		- 证明：
			- stage1: 加入新token前后，假设前i个token经过前j-1层decoder得到的上下文嵌入保持不变，证明第i个token经过第j层decoder得到的上下文嵌入保持不变
				- 因为前i个token的上下文嵌入保持不变
				- 所以前i个token的上下文嵌入在第j层投影成QKV没有变化
				- 第i个token计算前i个token地注意力分数，注意力权重没有发生变化
				- 第i个token得到的第j层的上下文嵌入未发生变化
			- stage2: 由stage1推理出i-1，i-2，...，1也是保持不变。得到加入新token加入前后，前i个tokens经过第j层decoder得到的上下文嵌入保持不变
			- stage3：由于第0层的token embedding是保持不变的，由数学归纳法得证。
	- 由上面那一条，引入i+1个token时，前i个的上下文嵌入都是知道的，对于预测下一个token，我们只需要知道i+1个token的上下文嵌入。对于计算第j层这个i+1token的上下文嵌入来讲，我们已经预先知道j-1层前i个token的上下文嵌入。哪儿些是可以复用的呢？本质上是每一层前i个token对应的嵌入是可以复用的，但是可以进一步复用对应的他们的KV，而不直接复用嵌入，这样可以省略KV的计算，然后就可以计算出第i+1个token对前i个的注意力分数，继而得到经过该层后的上下文嵌入。最后的前馈计算和softmax也只需要计算最后一个token的上下文嵌入即可。
		- 历史 token 的 K、V 缓存起来；
		- 计算新token得Q，K，V，（把KV缓存起来）
		- 计算新token对{历史 token, 新token}的注意力分数，继而得到上下文嵌入
		- 重复步骤 2～3，直到最后一层。计算该嵌入的前馈和softmax得到下一个预测结果。
3. Bert和GPT的本质区别是什么？
	- 尽管在结构上Bert和GPT都是由MHA和FFN构成，但是本质区别在Bert的MHA是双向自注意力，而GPT是因果自注意力，使模型以自回归方式建模序列。。这也导致了一个影响，序列中增加一个新的token，Bert得重新走一遍这个模型；gpt可以利用KV缓存，只跑最后一个token。
	- 自回归建模要求当前位置的预测不能利用未来 token 的信息，因此在 Transformer 中通常通过因果注意力（causal attention）来保证这一条件。
4. 如何理解注意力分数矩阵
	- 从行的角度看：第 i个 Query向量对各个 Key向量的关注程度
	- 从列的角度看：第j个key向量被各个Query向量的关注程度
5. 对decoder-only model的理解
	- step1: 通过掩码自注意力 + FFN，得到上下文嵌入
	- step2: 对最后一个token的上下文嵌入通过FFN + softmax得到下一个token的预测
		- 最后一层最后一个token的上下文嵌入的获得依赖n-1层1～m个上下文嵌入的获得
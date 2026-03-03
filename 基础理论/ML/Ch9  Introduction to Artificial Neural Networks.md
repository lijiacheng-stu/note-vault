## 一、相关历史
### 1. 为什么这次的人工智能浪潮不会像以前一样消失
- 能获取大量的**高质量数据**用于训练人工神经网络
- **算力的提升**使得在一个合理的时间内能完成模型的训练
- 人工神经网络理论上的**限制**，在实践中，被证明是**良性的**。局部最优解和全局最优解的性能和全局最优解几乎相同
- Transformer的发明。Transformer几乎能解决所有类型问题，因此可以训练非常大的基础模型，通过微调或提示就能复用到其他的任务。
- 人工神经网络进如何良性的融资和进步循环。

### 2.大事件
- （兴起）1943，Warren McCulloch 和 Walter Pitts第一次提出了人工神经网络。被认为很快能出现具有智慧的机器人，并与之交流。
- （衰落）1960s，前景段时间无法时间，投资消失。
- （兴起）1980s，新的架构被发明。
- （衰落）新的架构的进展缓慢，1990s，更好的机器学习算法被提出，他们有更好的效果和理论基础，因此神经网络的研究又停滞了。
- （兴起）当前，5大理由，又兴起了，且不会消失。

## 二、生物神经元
### 1. 组成
- cell body 细胞体
- dendrite 树突 /ˈden.draɪt/
- axon 轴突 `[ˈæksɑn]`
- telodendrion 轴突终末分支
- synaptic terminals 突触末端 或 突触小体
- action potential 动作电位
- neurotransmitter 神经递质
### 2. 行为
- 动作电位通过轴突传递，并使得突触小体释放神经递质。当一个神经元在短时间内接受了足够多的神经递质，它将启动它自己的动作电位。（也存在抑制动作电位的神经递质）
### 3. 图像
![[Pasted image 20260303161006.png]]
![[Pasted image 20260303161250.png]]
## 三、感知机perceptron
TLU = threshold logic unit 阈值逻辑单元
### 1. TLU
#### 1.1 组成
- step function 阶跃函数 （又是激活函数之一）
- linear function 线性函数
#### 1.2 作用机制
- input：$\mathbf{x}$
- output：$h_\mathbf{w}(\mathbf{x}) = \operatorname{step}(\mathbf{w}^T \mathbf{x} + b)$
#### 1.3 注意
1.3.1 step指代阶跃函数，具体的函数是如下：
	- Heaviside step function /ˈhevɪsaɪd/ （最常见）
	-  sign function 
1.3.2 一个TLU的参数是：$\mathbf{w}和b$
1.3.3 结构图：
![[Pasted image 20260303164233.png]]
### 2. Perceptron
2.1 定义：
-  _fully connected layer_, or a _dense layer_：A perceptron is composed of one or more TLUs organized in a single layer, where every TLU is connected to every input.
2.2 相关知识点：
-  invented in 1957 by Frank Rosenblatt
- The perceptron training algorithm proposed by Rosenblatt was largely inspired by _Hebb’s rule_.
2.3 特点
- efficiently compute the outputs of a layer of artificial neurons for several instances at once.
![[Pasted image 20260303165233.png]]
- 输出的结果的形状：m * n
- 第k个实例的第j个TLU的输出结果：X的k行，W的j列 + b的j列，对这个求激活函数
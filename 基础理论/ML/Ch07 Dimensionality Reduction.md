## The curse of Dimensionality
1. curse of dimensionality：Many machine learning problems involve thousands or even millions of features for each training instance. Not only do all these features make training extremely slow, but they can also make it much harder to find a good solution

2. 讲的是降维的必要性，以及维度灾难的原因：
- some types of models will not be usable at all because they scale poorly with the dataset’s dimensionality (e.g., SVMs or dense neural networks).
	- 复杂度随着n增长得很快的意思
 - high-dimensional datasets are often very sparse：
	-  -->patterns in the data will become harder to identify, models will tend to fit the noise more frequently than in lower dimensions;
		- most training instances are likely to be far away from each other, so training methods based on distance or similarity (such as _k_-nearest neighbors) will be much less effective.
			- 距离近也不一定真的近，用距离度量的区分度下降
		- new instances will likely be far away from any training instance, making predictions much less reliable
	- -->models will become even harder to interpret.
解决方案：
- 增加训练集的数量，但是不可行：With just 100 features—significantly fewer than in the MNIST problem—all ranging from 0 to 1, you would need more training instances than atoms in the observable universe in order for training instances to be within 0.1 of each other on average, assuming they were spread out uniformly across all dimensions.
- 降低维度：
	- speeding up training
	- possibly improving your model’s performance
	- extremely useful for data visualization
## PCA
魔鬼细节：
- 在数学中，有独立意义的向量，以列向量方式存储在矩阵中
- 在sklearn中的api风格，有独立意义的向量，以行向量方式存储在矩阵中
理论基础：为什么要优先选择保留最大方差的轴？
- project
-  to select the axis that preserves the maximum amount of variance, as it will most likely lose less information than the other projections.
- it is also the axis that minimizes the mean squared distance between the original dataset and its projection onto that axis.
定义：
- first principal component（PC):
	- the axis that accounts for the largest amount of variance in the training set. 能解释最大数量的方差的轴 
- Principal Component Vector:
	- the zero-centered unit vector lies on first principal component, 记为$c_1$
算法：
- 对X逐特征地进行中心化，sklearn提供的PCA的fit中会自己中心化。
- 找到X的前d个主成分，并得到他们的主成分向量：
	- 先找第一主成分
	- 在第一主成分垂直的方向找，找能解释最大数量方差的轴，作为第二主成分
	- ... ...
	- 找到满足需求数量的第d主成分
- 将n维的X向下投影到d维，得到$X_{d-proj}$
算法基础：
- 怎么得到第i主成分向量：
	- 奇异值分解SVD：$X = U\Sigma V^T$，X的主成分向量会在V中，第i列是第i主成分向量。$V=[c_1,c_2,...,c_n]$
- 怎么向下投影：
	- $X_{d-proj}=XW_d$ ，其中，$W_d = [c_1,c_2,...,c_d]$
- 怎么知道需要投影多少个维度：
	- 方法一：
		- 计算各个主成分的方差解释率 （explained variance ratio）
			- Explained Variance Ratio的计算就是：对X逐列计算方差再求和得到总方差。对X在第i主成分上投影得到的z1，z2,..,zm求方差得到这个这成分的explained variance。最后用explained variance / 总方差
		- 设定一个目标解释率，例如0.95。然后选择前d，使得刚好超过0.95。
	- 方法二：绘制一个dimension-explained variance的图像，找到一个拐点，次后，再增加维度对方差解释率的提高影响不大。
	- 方法三：作为一个超参数，用SearchCV来找
```
对奇异值分解的理解：
sigular value decomposition: $X = U\Sigma V^T$
- $X_{m*n}$，即X中的instance是在n-dimension的 --> n个主成分--> 每个主成分由一个单位向量表征，这个向量在n-dimension中--> 单位向量是n维度 --> 由n个用于表征主成分单位向量构成的矩阵$V$是$n*n$的
- 主成分选择是，先选择第i个后，第i+1个的选择必然是垂直于前i个单位向量的--> 彼此正交，又均是单位向量 --> 单位正交矩阵，但不一定是对称矩阵
- $V$是把每一列认为是主成分单位向量，可是在SVD中，要求每一行是主成分单位向量，因此，$V^T$
```
其他：
- 可以decompress
- 可以Incremental PCA

## Random Project
理论基础：
- the random projection algorithm projects the data to a lower-dimensional space using a random linear projection.This may sound crazy, but it turns out that such a random projection is actually very likely to preserve distances fairly well.
	- two similar instances will remain similar after the projection, and two very different instances will remain very different.
算法：
- 确定需要投影的维度d，算法是$d ≥ 4 log(m) / (\frac{1}{2}\epsilon^2-\frac{1}{3}\epsilon^3)$,当然也可以自己指定
- 随机初始化P矩阵，矩阵`d*n`,表征d个实例空间中的主成分向量。初始化要求均值为0，方差1/d的正太分布（GaussianRandomProject）
	- 若是SparseRandomProject，对于P中每一个cell有r （density，矩阵非零的占比）概率非零，若非零选择–_v_ or +_v_ (both equally likely), where _v_ = $v = 1/\sqrt(dr)$,不服从正态，但是保证了均值和方差
- X @ P.T  

## LLE
- manifold learning
- distances between instances are locally well preserved. However, distances are not preserved on a larger scale


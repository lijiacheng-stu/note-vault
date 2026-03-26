## The curse of Dimensionality
讲的是降维的必要性：
 high-dimensional datasets are often very sparse：
- -->most training instances are likely to be far away from each other, so training methods based on distance or similarity (such as _k_-nearest neighbors) will be much less effective.
- --> some types of models will not be usable at all because they scale poorly with the dataset’s dimensionality (e.g., SVMs or dense neural networks).
- -->new instances will likely be far away from any training instance, making predictions much less reliable
-  -->patterns in the data will become harder to identify, models will tend to fit the noise more frequently than in lower dimensions;
- -->models will become even harder to interpret.
解决方案：
增加训练集的数量，但是：With just 100 features—significantly fewer than in the MNIST problem—all ranging from 0 to 1, you would need more training instances than atoms in the observable universe in order for training instances to be within 0.1 of each other on average, assuming they were spread out uniformly across all dimensions.


X m * n --> instance in n-dimension --> unit vectors that define all the principal component in n-dimension
V = (c1, c2, ..., cn) --> 有n列 --> 一行一个unit vector，而不是一列 -- > 最多拥有n个unit vector, 因此V是n * n的矩阵 --> 难道v不能是一个对称矩阵吗？
X_d-proj = XW_d --> 能乘--> W_d是经过转置的

对奇异值分解的理解：
sigular value decomposition: $X = U\Sigma V^T$
- $X_{m*n}$，即X中的instance是在n-dimension的 --> n个主成分--> 每个主成分由一个单位向量表征，这个向量在n-dimension中--> 单位向量是n维度 --> 由n个用于表征主成分单位向量构成的矩阵$V$是$n*n$的
- 主成分选择是，先选择第i个后，第i+1个的选择必然是垂直于前i个单位向量的--> 彼此正交，又均是单位向量 --> 单位正交矩阵，但不一定是对称矩阵
- $V$是把每一列认为是主成分单位向量，可是在SVD中，要求每一行是主成分单位向量，因此，$V^T$


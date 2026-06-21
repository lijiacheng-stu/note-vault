- canonical 规范的 /kəˈnɒnɪkl/
- Inception

我们展示了卷积和深度可分离卷积位于离散频谱的两端，而Inception模块位于中间。


通过Xception和Inception的比较，我觉得“We showed how convolutions and depthwise separable
convolutions lie at both extremes of a discrete spectrum,
with Inception modules being an intermediate point in be-
tween. ”是有问题的：
- Inception是通过先跨通道，来分离多个分段，每个分段有多个通道，然后让正常卷积在各个分段上使用。且跨通道和正常卷积存在非线性函数
- 推测xception的结构：先跨通道，来分离多个分段，每个分段有一个通道。，然后让正常卷积在各个分段上使用。且跨通道和正常卷积存在非线性函数
- 实际上的xception的结构：先逐通道的用正常卷积，然后再夸通道，最后取消了中间的非线性函数。

文章认为这种交换是不重要的；然后还比较了有无激活函数，发现没有还更好。因此，就等价了。

这里有个核心的观点，说Inception可以认为是介于depthwise separable conv 和 regular conv之间的中间态。他们的本质都是先划分通道，然后在每个分段上，再用普通卷积。本质区别是通道划分方式。regular conv，就是一整个都是；depthwise separable conv 就是一个通道一个分段；inception就是多个通道一个分段。

## 其他信息
- 原图像的shape是(224, 224, 3)
- 低级特征的特征图的shape是(56, 56, 256), 即output stride=16
- DeepLabv3特征图的shape是(14, 14, 256)，即output stride=4
![[Pasted image 20260624225706.png]]

## 基本信息
- 会议论文：ECCV
- 2018年
- Google
- WoS：11497
## 引言
贡献：
- 提出了一个创新的编码器和解码器结构
- 



问题：
- 问题一：atrous convolution 是如何任意控制提取的编码器特征的分辨率的？
- 问题二：为什么要使用atrous convolution？
- 问题三：为什么要使用编码器-解码器结构？
- 问题四：spatial pyramid pooling，为什么当时要求图片固定尺度，和fcn有什么关系？SPP指的到底是一个特征图被多种类型的操作处理再拼接？还是输入任意尺度的特征图，输出固定尺度的特征图？原文是怎样操作的？
- 问题五：DeepLabv3中ASPP module是否也采用了depthwise separable convolution?
- DeepLabv3+是如何将depthwise separable convolution 用于decoder的？

对问题一：
- 原model是分stage，每个stage输出一个特定空间尺度的特征图，stage的第一个block会通过stride、pooling等操作实现下采样，降低空间分辨率
- 现在要控制OS=16，就找到原模型输出OS=16分辨率的stage，然后这个stage的后继stage，使得其stride=1, 空洞卷积rate=2，实现。
- 上面的调整不会改变模型的参数，保证了相同的感受野，增加了推理时间。

对问题二：
- 通过atrous convolution能够提取更密集的特征图，在减少由于stride或者池化操作引起关于物体边界的细节信息的损失的同时，保持感受野，从而使输出特征图保持同样丰富的语义信息。但是，会引起计算复杂度的提升，对ResNet而言，16比较适中，8影响太大。

对问题三：
- encoder-decoder structure, 能够通过逐渐恢复空间信息来获得更加清晰的边界

对问题四：
- 在2014年SPPNet没有提出之前，经典的卷积网络的结构都是CNN+FCN。最后一个CNN特征图如何输入到FCN呢？有两种做法，第一种是将(H,W,C)的特征图展平，第二种是在空间维度进行池化得到C向量。对于前者，要求输入的图片尺寸必须的固定的；后者尽管可以输入任意尺度的图片了，但也损失了过多的信息。那怎么才能可以接受的信息损失的范围内，可以输入任意尺度的图片呢？SPPNet给出了答案。SPP（Spatial Pyramid Pooling）不再仅仅执行一次全局池化，而是将输入的特征图在空间维度上按照不同粒度进行多尺度划分，例如粗粒度（1×1）、中等粒度（2×2）以及细粒度（4×4）。在每一个尺度下，特征图被划分为若干个 **spatial bins（空间划分单元）**，这些 bin 在空间上按照输入特征图的宽高进行**近似等比例划分**，从而保证不同输入尺寸下仍能保持结构一致性。在每一个 spatial bin 内部，分别进行池化操作（如最大池化或平均池化），以提取该区域的特征表示。由于不同尺度对应的 bin 数量不同，最终将所有尺度下得到的池化结果按顺序拼接，形成一个固定长度的特征向量，用于后续的全连接分类层。
- 上面包含了两个思想，不同尺度的图像可以输入网络了；同一个特征图进行多尺度的操作，最后将结果进行拼接，这是这个文章继承的思想。
![[Pasted image 20260625122746.png]]


对问题五：
- depthwise separable convolution = depthwise convolution + pointwise convolution ≈ standard convolution，它的作用是能够用更少的参数，更少的计算，达到甚至超越标准卷积操作的性能。
	- 如输入特征图(H1, W1, C)，输出(H2, W2, D),卷积核`k*k`,需要学习多少参数呢？
		- 对depthwise separable convolution：`C*k*k+C*D`
		- 对于standard convolution：`D*C*k*k`
- 逐深度可分离卷积可以丝滑替换标准卷积，所以并不是必须的，DeepLabv3中ASPP module并没有采用。









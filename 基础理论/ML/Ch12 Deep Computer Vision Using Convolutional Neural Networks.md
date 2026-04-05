## 1. **visual cortex** vs **CNN** 
- 每个神经元对应一个局部感受野：一个位于给定层的给定位置的神经元连接到位于它前一层的f_h,f_w长宽的一个矩形区域内的所有神经元的输出。
- 不同神经元的感受野可能不同，但可能存在重叠：stride < min{f_h, f_w}时，给定层的给定位置的神经元与它相邻位置的神经元，一定存在感受野的重叠
- 不同神经元对相同方向的线条有不同响应，对特定方向的线条更敏感：在相同spatial dimension上有多个神经元，这些神经元有不同的weight和bias，有相同的local receptive field，这使得不同神经元对相同方向的线条产生不同响应，对特定方向的线条更敏感。然后每个sptial dimension都放置所有这些类别的神经元，同种类别的神经元或他们的输出形成一个feature map，这体现了同一feature map上的神经元共享权重。

## 2.Pytorch处理图片的兼容性分析
- Pytorch对图片的要求：
	- C * H * W
	- 0～1，dtype=torch.float32
- imshow对图片的要求：
	- H * W * C
	- 0～255 int 或 0～1 float
	- 若是float，超过1 的部分被截断
- torch.permute(), 用于转换axis，用于兼容不同的库对channel所处dim的要求

## 3. 卷积神经网络的理解
我现在对convolutional layer产生了三种理解：
- 第一种，以神经元为核心：
	存在诸多神经元，这些神经元依附在feature map上，不同feature map上的神经元的weight和bias不同，相同feature map上的神经元相同。不同神经元有不同的local receptive field。
- 第二种，以卷积核为核心：
	存在多个卷积核，每个卷积核以kernel size，stride对图像进行卷积操作，每个不同卷积核能产生一个feature map。
- 第三种，把convolutional layer看成是dense layer + 滑动扫描：
	如feature maps的数量是n，则convolutional layer就是一个n个神经元构成的一个dense layer，他们通过滑动处理图片，每次处理local receptive field那么大的input features。数学形式上是统一的。
	多个convolutional layer堆叠的情况，能够看成feedforward neural network对图片的扫描呢？一般的不行。第一层是n个神经元，产生n个输出，根据dense layer的规则，后一层输入应该是n个维度，因此，第二层的神经元只能使得其local receptive field = 1 * 1，事实上，并不是这样的。

## 4. Layer blocking backpropagation
```
x1 = torch.tensor(1.0, requires_grad=True)
x2 = torch.tensor(2.0, requires_grad=True)
x3 = torch.tensor(3.0, requires_grad=True)

f1 = x1 * x2
f2 = f1 + x3
f2_detached = f2.detach() # （*）
f3 = f2_detached + x1
```
要理解阻断反向传播层，就是要理解`(*)`式。
- f2.detach()之后，返回的是与f2共享内存的tensor对象f2_detached，这个对象requires_grad属性为False。当f2_detached这样的对象，与requires_grad为True的x1参加计算时，autograd在绘制计算图时，仅仅存入f2_detached的数值。所以对于f3绑定的计算图对象的视角来看，它的上游节点一个是数值，一个是AccumulateGrad，在反向传播时，到x1处即结束。
- 到f2处，仅进行了前向传播，还可对f2进行反向传播。


## 5. CNN Architectures
### AlexNet
-  ILSVRC 2012 challenge， 17%
- it was the first to stack convolutional layers directly on top of one another
- regularization techniques：`/ˌreɡjələraɪˈzeɪʃən/`
	- dropout
	- data augmentation:
		- 数据集上的数据增强：
			- 对图片可进行的增强操作
				- **slightly shift, rotate, and resize** every picture in the training set by various amounts and add the resulting pictures to the training set
				- **tweak the colors, and contrasts** to simulate many different lighting conditions.
				- **flip the pictures horizontally**
				- combining these transformations
			- 使用场景：
				- 增强模型的鲁棒性
				- unbalanced dataset， SMOTE
				- _test-time augmentation_ (TTA)
	- local response normalization： This encourages different feature maps to specialize, pushing them apart and forcing them to explore a wider range of features, ultimately improving generalization.
### GoogLeNet
-  ILSVRC 2014 challenge，below 7%
- inception module
	- 简单理解：a convolutional layer on steroids
	- allow GoogLeNet to use parameters much more efficiently than previous architectures
	- 1 × 1 kernels：
		- Although they cannot capture spatial patterns, they can capture patterns along the depth dimension (i.e., across channels).
		- bottleneck layers：cuts the computational cost and the number of parameters, speeding up training and improving generalization.
		- Each pair of convolutional layers (`[1 × 1, 3 × 3]` and `[1 × 1, 5 × 5]`) acts like a single powerful convolutional layer, capable of capturing more complex patterns.

### ResNet
-  ILSVRC 2015 challenge，under 3.6%
- skip connections 跳跃连接：
	- When training a neural network, the goal is to make it model a target function _h_(**x**). If you add the input **x** to the output of the network (i.e., you add a skip connection), then the network will be forced to model _f_(**x**) = _h_(**x**) – **x** rather than _h_(**x**). This is called _residual learning_
	- If the target function is fairly close to the identity function (which is often the case), this will speed up training considerably.
	- if you add many skip connections, the network can start making progress even if several layers have not started learning yet (see [Figure 12-17](https://learning.oreilly.com/library/view/hands-on-machine-learning/9798341607972/ch12.html#deep_residual_network_diagram)). Thanks to skip connections, the signal can easily make its way across the whole network. The deep residual network can be seen as a stack of _residual units_ (RUs), where each residual unit is a small neural network with a skip connection.
### xception
- Depthwise separable convolutional layer
- Separable convolutional layers use fewer parameters, less memory, and fewer computations than regular convolutional layers
	- the numbers of parameters in **regular convolutional layer**  and **separable convolutional layer**，with the same in_channels, out_channels, kernel_size:
		- for regular convolutional layer: `in_channels * kernel_size * kernel_size * out_channels + out_channels`
		- for separabel convolutional layer: `in_channels * kernel_size * kernel_size + in_channels + in_channels * out_channels + out_channels`
		- regular convolutional layer - separabel convolutional layer = `in_channels * kernel_size * kernel_size * (out_channels - 1) - in_channels - in_channels * out_channels`
- note that `in_channels` and `out_channels` need to be divisible by `groups`
	- `in_channels` 要能均分成groups组，因此需要被整除
	- 当`groups = 1`时，为normal convolutional layer，此时，每个group对应out_channels个filters
		- 合理推断：当`groups = k`时，由于`out_channels` 个feature maps，因此只能有`out_channels` 个卷积核，每一组均等，因此，每一组应该是out_channels / k个卷积核。因此，out_channels要能被k整除。
	- 特殊地，`groups = in_channels, out_channels = in_channels`时, 每组一个channels，每组一个kernel，从而形成depthwise convolutional layer
- depthwise max pooling 和 depthwise convolutional layer 和 depthwise concatenation和Pointwise convolution
	- depthwise max pooling中，depthwise指的是沿着channel这个dim，进行max pooling操作
	- depthwise convolutional layer中，depthwise指的是每一层为一个单位，分别进行卷积操作
	- depthwise concatenation中，不同的input，在channel这个dim进行拼接
	- Pointwise convolution，pointwise指的是kernel的size是`1*1`的。
	- 疑问： depthwise max pooling 的语义和Pointwise convolution很接近
### SENet
- ILSVRC 2017 challenge，2.25%
- 
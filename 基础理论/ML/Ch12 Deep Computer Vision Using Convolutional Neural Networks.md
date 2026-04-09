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


## GPU RAM Requirements: Inference Versus Training
1. 要描述一个卷积层，至少需要5个参数：
	- the number of feature maps (out_channels)
	- kernel size
	- stride
	- padding
	- the number of channels of previous layer(in_channels) 
2. a single convolutional layer with 200 5 × 5 filters, stride 1 and `"same"` padding, processing a 150 × 100 RGB image (3 channels):
	- 参数的数量 `(5 * 5 * 3 + 1) * 200 = 15,200`,即59kB
	- 输出一次feature map需要进行的浮点数乘法计算：`(5 * 5 * 3) * 150 * 100 * 200 = 225 million`
	- 输出的feature map所占据的空间：`4 * 150 * 100 * 200 = 11.4MB`
	- 若是100个instance一起处理，则为1GB左右
3. 推理过程：
	- 所有的参数
	- 存储连续的两层的feature map
4. 训练过程：
	- 所有的参数
	- 所有层计算出的feature map （用于反向传播）
5. 结论：
	- 训练阶段比推理阶段需要更多的内存
		- 训练阶段会使用batch，包含多张图片，推理阶段可以少量的几张
		- 训练阶段的所有中间结果feature map都要存储
	- 在推理阶段处理一张图片需要的内存是两个feature map的所需容量


## Implementing RU and ResNet34
### 1.总体思路
- 在构造器中写出各个模块
	- skip connection
	- main layers
- 在forward中，把各个模块串联起来
### 2. 魔鬼细节
- 继承nn.Module, 构造器中使用`super().__init__()`
- 所有的covolutional layer中的神经元的bias = 0, 因为后面紧跟着BN，BN中可学习的beta就相当于时bias了
- inputs来表达输入，而不是input，因为input是哪只函数名
- 在forward中，需要对result1 + result2的结果进行relu，这里不需要先用nn.Relu()(result1 + result2)。因为relu是一个逐元素操作，直接使用函数就行，torch.nn.functional.relu。
- 使得输出和输出不匹配的原因，不仅仅是stride使得H，W不匹配，还有可能是in_channels,和out_channels不同。且stride>1时往往伴随着out_channels加倍，因此，if stride > 1 or out_channels != in_channels:
- 对于ResNet34中，34指的是卷积层和全连接层的数量，第一个convolutional layer的padding = 3
### 3.遇到的困难
困难点1: nn.BatchNorm1d还是nn.BatchNorm2d，有什么区别？
困难点2: nn.Conv2d还是nn.Cov3d, 有什么区别? 
困难点3: 对相同的img做这两个卷积操作，128, 1 * 1 + 2(S) 和128， 3 * 3 + 2（s）特征图的维度H，W一定会相同？

ans1:
- BatchNorm = batch normalization 批归一化
- 公式的第一步用的是标准化, 却用的是norm，归一化
	- $$y = \frac{x - \mathrm{E}[x]}{\sqrt{\mathrm{Var}[x] + \epsilon}} * \gamma + \beta$$
- 对C这个维度做计算均值和方差，并逐元素归一化
	- 1d：空间维度是1，单个instance的指定c后的索引结果是1d的，所以输入的形状是(N, C, L), 计算C次归一化，每次统计的均值和方差是`input[:,c,:]`索引得到的元素。特殊地，当L=1时，输入的形状变为(N,C)
	- 2d：空间维度是2，单个instance的指定c后的索引结果是2d的，索引输入形状(N, C, H, W), 计算C次归一化，每一次统计的均值和方差是`input[:,c,:,:]`索引所得到的元素。
- 输入和输出形状相同

ans2：
- Applies a 2D convolution over an input signal composed of several input。
	- 2D convolution：在二维输入平面上，用一个较小的二维核（kernel）滑动，对每个局部区域做加权求和，得到输出特征图。
	- 2D指的是卷积核滑动的维度

ans3:
- $H_{out}$ , `height of output`跟$H_{in}, P, S, K$,`, height of input,padding,stride, kernel_size` 有关公式是：
![[Pasted image 20260407215804.png]]
- 因此可以得到skip_connection的p=0

## 使用预训练模型
来源：
- TorchVision
- TIMM
- Hugging Face

形容模型大小的词：
- tiny
- small
- base
- large

基本的问题：
- 探究基本问题：
	- 能下载哪儿些模型？
		- torchvision.models.list_models() --> list of 'model_name'
	- 这些模型有哪儿些可选的参数？
		- tochvision.models.get_model_weights('model_name') --> 返回这个模型能够使用的参数名称的枚举容器，容器中包含了这个模型可能的针对其他数据集或训练方法的多个权重版本。
		- 容器中特定的权重版本，暂且标记为weights：
			- weights不包含具体的权重，但是有权重所在的地址。具体看`weights中有什么？`
	- 下载的参数缓存在了哪儿里？
		- torch.hub.get_dir()
	- 这些模型有哪儿些功能？
		- 用jupyter lab中的`?` ，或者的`__doc__`查看`torchvision.models.model_name`
	- 创建实例，并为实例传入预训练参数
		- 获取参数版本：“枚举容器 + 具体版本” 
			- get_model_weight()获得枚举容器，再指定具体版本
			- torchvion.model也存储了参数的枚举容器，可通过get_model_weight()知晓名称，再指定具体版本
		- 用torchvision.models.list_models()返回的模型名，一定存在相应的创建该模型实例的函数torchvision.models.model_name(),这个函数可以内部自动进行如下操作：
			- 下载权重(option)，依赖weight的url属性
			- 创建模型实例
			- 把权重载入模型实例等(option)
- weights中有什么？
	- value
		- url, 模型的参数的位置 --> get_state_dict方法依赖此属性--> 用于得到模型的参数，然后传给实例
		- transforms, 预处理函数对象 --> transforms方法依赖此属性--> 用于预处理 --> 包装成方法的可能原因是防止可能不需要的对象占用内存，动态地生产对象
		- meta，模型的描述 --> meta属性依赖此属性
			- 'num_params'，参数数量
			- `_file_size`,path的文件大小
			- `'_metrics'`，预测能力
			- `recipe`，训练方法
	- 所谓的其他方法都依赖于value的值，这也体现了Enum的设计哲学
基础知识：关于Enum
- 在weights中的结构
```python
from enum import Enum
class WeightEnum(Enum):
	WEIGHT_V1 = value1
	WEIGHT_V2 = value2
	WEIGHT_V3 = value3
	
	def __init__(self):
		self.curl = self.value.curl
		self.meta= self.value.meta
	
	def get_state_dict(self):
		```依赖value中的curl，包括从网上下载权重到本地cache，封装成一个字典```
	
	def transforms(self):
		```依赖value中的transforms，调用value点transforms()```
```
所以，当使用`WeightEnum.WEIGHT_V1`时，天然地有'get_state_dict','meta', 'name', 'transforms','url','value'
- 对enum对象，应该知道至少有name，value属性，还可能有其他依赖于value的属性和方法。
- 方法和属性都能返回对象，属性是静态的，方法是动态的，省内存。

## Pretrained Models for Transfer Learning
### 基本的问题
- 怎样替换已经创建的模型实例的部分模块？
- 怎么冻结模型的参数？
- 怎么先冻结一部分，在逐渐地解封？


更基本：
- 如何解构模型和他的参数？
	- 模型有两种构成类型, 一种是由子模块构成的模型，另一种是由参数构成的模型。他们都是离散地定义在构造器中。在forward函数中，将他们串联起来，形成一个有机的结构，从而实现反向传播调整参数，已经前向传播做出预测。
	- 只有nn.Parameter类型，和nn.Module类型的属性，才能model.to(device)是被传到对应的芯片, 被parameter(),children()方法找到
	- 构造器中，`self.xx`,形成模型的属性，这些属性中有两个是特别的属性，一个是Parameter类型，一个是Module类型。
	- 对于model.parameters()/named_parameters()返回一个iterator对象：
		- 找到Parameter类型的属性，放进去
		- 找到Module类型的属性，对这个model执行parameters()，递归。
			- 检索路径就会是named_parameters()中的名字
		- 名称就是属性名，值就是参数
	- 对于model.children()/model.named_children()返回一个iterator对象：
		- 找到Module类型的属性，放进去，非递归。
		- 名称就是属性名，值就是模块。属性名可以用model.attribute来获得值。
	- model.parameters()的iterator对象，和模型内部的有什么关联？
		- 内容物，指向的参数和模块都是model中同一个，可以实现inplace操作，无法实现对model的替换。
		- 
- 如何构建数据加载器？分离所谓的feature和target
	- Dataset实现了__getitem__()和__len__()方法，其中`ds[i]`,返回结果是一个元组，第一个是X，第二个是y。（当然也可以是三元组）
	- Sampler依赖data，返回可迭代对象，里面是针对data和sampler策略的索引
	- DataLoader：按照sampler提供的索引顺序，按照batch_size的尺度，提供数据
- 如何用pytorch的optimizer ，schedule等等训练模型？
- 如何逐渐解冻一部分？

四类评价指标：
- during each epoch, use batch in training set:
	- 记录每个batch的loss，最后加和 / m，得到平均loss，判断模型的波动情况
- at end of each epoch, use training set and validation set：
	- 用训练集和验证集测试性能，判断是否过拟合。
- at end of training using training set, use validation set：
	- 用验证集测试性能，用于评估当前训练的模型的性能，选超参数和模型。
- end of training using training set + validation set, use test set to measure the ability of model:
	- 用测试集，评估模型性能和泛化能力
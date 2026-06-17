Depthwise separable convolution = depthwise convolution + pointwise convolution
- 效果上约等于standard convolution，但是有更低的计算复杂度

提高计算效率的方法：
- bottleneck layer
- Depthwise separable convolution, factorizing a standard convolution into a depthwise convolution followed by a pointwise convolution

同时让多尺度特征图同时包含空间和语义信息的方法：
- HRNet
- FPN， U-Net？


捕捉上下文信息的四种方法：


想要大的感受野，但是不想stride的做法





spatial pyramid pooling指的到底是什么，是一张特征图被多个不同感受野的filters处理，还是让游让多张不同空间尺度的特征图产生相同尺度的输出？



空洞卷积的理解：
- 要提高“感受野”，目的是上下文整合，正常的操作是，池化或stride>1 + 正常卷积。这样的结果是输出分辨率比输入的更低，降低了精确定位。怎样才能保证输入输入分辨率相等（保持一定的精确定位），又能有大的“感受野”的？把卷积核做大，但导致计算量增常太多；把卷积核做大，且其面用很多0占位，即空洞卷积。


你判断一下，我对Loss的理解是否地道。分两种情况看待loss，一种是已知(predict，target， 其他的正则要求)，未知loss；第二种是已知loss，(predict，target，正则要求未知)：
- 对第一种情况，应用场景是Loss的设计。有个总体的要求，模型性能越好，Loss需要越小。性能好坏的评价指标是得模型设计者自己把握的，它能引导模型的学习方向。针对（predict，target）项，往往设计一个损失项Loss1，用来衡量predict和target接近程度。设计一个接近的标准，然后逐实例地计算loss，再相加得到Loss1。当然正则要求往往会渗透到Loss1的设计，而不单独成项。
- 第二情况，应用场景是Loss的解读，目的是辨析出接近标准和正则要求。一个方法是令Loss降低，看因变量的大小变化。可以逐Loss_i，进行分析。列出一个表格，index是Loss_i,columns时是变量，值是上下变化的箭头。如果对某个变量，箭头都相同，表明，模型鼓励什么。如果存在上下箭头，则存在权衡。 
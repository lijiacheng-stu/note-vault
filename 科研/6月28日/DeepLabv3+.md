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

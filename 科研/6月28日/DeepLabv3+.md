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


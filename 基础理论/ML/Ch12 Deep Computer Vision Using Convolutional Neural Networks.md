**visual cortex** vs **CNN** 
- 每个神经元对应一个局部感受野：一个位于给定层的给定位置的神经元连接到位于它前一层的f_h,f_w长宽的一个矩形区域内的所有神经元的输出。
- 不同神经元的感受野可能不同，但可能存在重叠：stride < min{f_h, f_w}时，给定层的给定位置的神经元与它相邻位置的神经元，一定存在感受野的重叠
- 不同神经元对特定方向的线条有响应：在给定层的给定位置设置多个不同的神经元，每个神经元对应特定的权重，叫做filter，如horizontal line filter，或vertical line filter，filter对线条的不同方向有不同的响应。同相同filter的一套神经元的输出，形成一个feature map，有多套，从而形成多个feature map。
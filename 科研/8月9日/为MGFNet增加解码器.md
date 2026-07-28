python scripts/train.py --cfg configs/MGFNet_YESeg.yaml
## 版本1:  简化版UNet decode style
- 用双线性插值替代deconvolutional network
具体设计：
- 对自上而下的特征通道数减半，上采样，使其空间分辨率与自下而上的特征相同，得到F1
- F1与自下而上的特征在通道维度进行拼接，得到F2
- 对F2进行两次`3*3`卷积，第一次通道数减少半，第二次不变
NFM ：相邻尺度特征融合模块

超参数提取：
- 分辨率倍增，是直接通过对自下而上的特征对w，h参数的提取实现。这可以在forward的时候，直接完成
- 通道数减少半，需要超参数，用目标通道数来比描述

### full_v2
![[Pasted image 20260728001346.png]]

### full_v1
![[Pasted image 20260728160810.png]]
### half_sar
![[Pasted image 20260728160848.png]]
### half_opt
![[Pasted image 20260728160908.png]]
### article
![[Pasted image 20260728160747.png]]

## 版本2： UNet decode style
- deconvolutional network
- Fully Convolutional Networks for Semantic Segmentation
- YOLO


### Knowledge
数据集的组织形式：
- 文件夹作lable
- 文件名作lable
- 两个文件夹，第一个文件夹存数据，第二个文件夹第一个文件数据的坐标以及其对应的lable
四元组：torch.ones((四元组))    (batch_size,channels,highth,width) 
进行一次参数weights更新要进行的操作：
 - 计算当前梯度下的损失函数计算当前参数值下 loss = loss_fn(outputs, targets)
 -  清除梯度 optimizer.zero_grad()
 - 每个参数的梯度(反向传播，损失函数确定后才能确定梯度函数  loss.backward()
 - 对参数进行跟你更新 optimizer.step()
注：每个batch进行梯度下降算法，此时的参数令batch的损失函数值最小
### Warning
[现有网络模型的使用及修改_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1hE411t7RN?p=25&vd_source=b4170b6c6869322af631975acedea53f)
- p25 6:26 经检验没有安装scipy
loss = loss_fn(outputs, targets)中的loss是什么数据类型的东西
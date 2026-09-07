对参数的理解
- $\mu_B,\sigma^2_B$
	- 对输入进行处理：
		- zero-centers
		- normalizes
	- 也是学习的，不过只跟输入有关，momentum是一个超参数
- $\gamma,\beta$
	- 对输出进行处理
		- scales
		- shifts
	- 在训练中学习的参数，用于拟合目标

对BatchNorm1d和BatchNorm2d的理解：
- 

## 一、words
- dual number 对偶数 $a + b\epsilon$

## 二、auto
### 2.Finite Difference Approximation
#### 2.1 前置知识
- $\displaystyle \frac{\partial f}{\partial x_i}(a_1,a_2,...,a_n)= \lim_{\epsilon \to 0} \frac{f(a_1,a_2,...,a_i + \epsilon,...,a_n)-f(a_1,a_2,...,a_n)}{\epsilon}\approx\frac{f(a_1,a_2,...,a_i + \epsilon,...,a_n)-f(a_1,a_2,...,a_n)}{\epsilon}|_{\epsilon=10^{-n}}$
#### 2.2 算法
- 目标：计算出$f(x_1,x_2,...,x_n)$在$(a_1,a_2,...,a_n)$处的梯度
- 做法：
	- 给$\epsilon$设定一个小的实数
	- 计算$f(a_1,a_2,...,a_n)$
	- 计算$f(x_1,x_2,...,x_n)$关于$x_1$在$(a_1,a_2,...,a_n)$处的偏导,$\displaystyle \frac{\partial f}{\partial x_1}(a_1,a_2,...,a_n)$
		- 计算$f(a_1,a_2,...,a_i + \epsilon,...,a_n)$
		- 计算$\lim_{\epsilon \to 0} \frac{f(a_1,a_2,...,a_i + \epsilon,...,a_n)-f(a_1,a_2,...,a_n)}{\epsilon}$
	- 类似地计算$x_2,...,x_n$
#### 2.3 分析：
- 计算次数：$f(a_1,a_2,...,a_n)$ 一次 + $f(a_1,a_2,...,a_i + \epsilon,...,a_n)$ n次 = n + 1 次
- 算法实现简单，往往用于检测其他的微分算法是否正确。

### 3.Forward-Mode Autodiff 前向模式自动微分
#### 3.1 前置知识
- $h(a+b\epsilon)=h(a)+bh(a)'\epsilon$，特殊地，当$b = 1$时, $h(a+\epsilon)=h(a)+h(a)'\epsilon$
- $\epsilon$非常小，因此，$\epsilon^2=0$
- computation graph 
#### 3.2 算法
- 目标：计算出$f(x_1,x_2,...,x_n)$在$(a_1,a_2,...,a_n)$处的梯度
- 做法：
	- 计算$f(x_1,x_2,...,x_n)$关于$x_1$在$(a_1,a_2,...,a_n)$处的偏导,$\displaystyle \frac{\partial f}{\partial x_1}(a_1,a_2,...,a_n)$
		- 用计算图计算$f(a_1+\epsilon,a_2,...,a_n)$，得到一个对偶数$a + b\epsilon$
		- 由于$f(a_1+\epsilon,a_2,...,a_n) = f(a_1,a_2,...,a_n) + \frac{\partial f}{\partial x_1}(a_1,a_2,...,a_n)\epsilon$，因此，b为此偏导数
	- 类似地计算$x_2,...,x_n$
- 结果：得到了$f$关于每一个$x_i$在$(a_1,a_2,...,a_n)$的偏导数，从而得到$f(x_1,x_2,...,x_n)$在$f(a_1,a_2,...,a_n)$处的梯度，实现目标。
#### 3.3 分析
- 计算的次数：每走一次计算图能够得到函数关于其中一个变量的偏导数，所以$n$个变量就是$n$次。
- 计算偏导的方向：从计算图的input的方向向output方向，所以是前向

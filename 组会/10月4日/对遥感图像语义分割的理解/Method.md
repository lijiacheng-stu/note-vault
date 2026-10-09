CSwin Transformer，对于第k个头的内含操作：
- 输入：原生的X，shape=`[H * W,C]`
- step1: 对X进行reshape，是的shape=`[H / sw, sw * W, C]`
- step2:对step1中，每个`[sw * W, d]`,分别投影成Q，K，V，继而作自注意力
- step3: reshape回`[H * W,C]`，等价于拼接操作。
注意：多头自注意力中，每个头的输入都是X，都执行了缩放点积注意力操作，但是区别是它们对X的投影不同。CSwin，reshape方式可能不同，有些是横向条带的，有些是纵向的，然后投影不同。
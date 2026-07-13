对gate fusion module（GFM）：
- $X^i_R$ 和$X^{i-1}_R$ 的空间分辨率是否相同？ 或 $X^i_{RDcom}$ 和$X^{i-1}_{RD}$ 的空间分辨率是否相同？
- gate 不是 一个通道一个数字那种了吗？

对global context module （GCM）：



对multilayer aggregation decoder (MAD):


step1：每个位置相对于其他所有位置的注意力。
step2: 得到每个位置的值。现在需要提供伟哥位置的值，就能得到最终的值。
step3: 每个位置的值 = 注意力 x 值
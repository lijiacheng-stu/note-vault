## 背诵
1. 对于 $Q$ 中的任意$Query$向量 $q_i$，通过分别与$K$中的所有$Key$向量进行点积运算，得到 $q_i$ 与各$Key$向量之间的**匹配得分**。这些得分经过缩放和 Softmax 归一化后，形成 $q_i$对各 Key 所对应位置或信息的注意力权重。
2. `[C1,C2,C3,C4,C5]`,对于Linear，操作矩阵的数量是1，作用单位是`[C5]`；对于Scaled Dot-Product Attention，操作矩阵的数量是3，即QKV，作用单位是`[C4_Q,C5_Q]`, `[C4_K,C5_K]`,`[C4_V,C5_V]`,其他通道相同，C5_Q = C5_K，C4_K=C4_V; 对于softmax默认与Linear相同；


Layer normalization (LN) is very similar to batch norm, but instead of normalizing across the batch dimension, LN normalizes across the feature dimensions.
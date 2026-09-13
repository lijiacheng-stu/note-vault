1. 概览

| 方面                      | 对应技术                                                                                                                         |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 加速生成式transformer的解码     | KV Cache，speculative decoding，parallelize text generation                                                                    |
| 加速MHA                   | sparse attention，approximate attention，sharing projections，FlashAttention                                                    |
| 加速达到数十亿参数的巨型transformer | mixture of experts                                                                                                           |
| 使大transformer的训练高效      | parameter- efficient fine-tuning ,PEFT(如，LoRA，activation checkpointing， sequence packing，gradient accumulation， parallelism) |
2. sparse attention的理解：一个token它都能感知到哪儿些token的信息呢？
	- 设S=0，且有N个NMA层存在
	- token本身能直接专注到的tokens，记录为S1，S = S + S1，依赖层数M = 1
	- 若S不等于所有token的集合，且S有更新，且N > ++M, 则遍历S中的每个token，每个token直接关注的token，并求并集，作为S2，S = S + S2，循环此步骤，否则退出循环。
	- 通过这个算法后，往往一个token其实能关注所有的token。
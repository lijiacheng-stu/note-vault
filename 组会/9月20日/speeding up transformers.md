| 方面                      | 对应技术                                                                                                                         |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 加速生成式transformer的解码     | KV Cache，speculative decoding，parallelize text generation                                                                    |
| 加速MHA                   | sparse attention，approximate attention，sharing projections，FlashAttention                                                    |
| 加速达到数十亿参数的巨型transformer | mixture of experts                                                                                                           |
| 使大transformer的训练高效      | parameter- efficient fine-tuning ,PEFT(如，LoRA，activation checkpointing， sequence packing，gradient accumulation， parallelism) |
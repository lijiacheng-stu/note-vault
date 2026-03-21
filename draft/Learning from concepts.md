ConText-CIR: Learning from Concepts in Text for Composed Image Retrieval
## Introduction
1. 基于图像和基于文本的图像检索和cir(组合图像检索)的区别
	- text-based:visionlanguage models such as CLIP [45], which have aligned image and text representations, have facilitated the text-based approach
	- Recent work in multi-modal image retrieval aims to mitigate these inherent limitations of uni-modal queries by introducing the composed image retrieval (CIR) problem

## 2 方法
2.1 问题设置（什么是CIR(组合图像检索)）
- 在一个候选图像库（gallery images）中，找到与查询最匹配的目标图像：该查询由一张查询图像(query image)和一段相关文本（relative text）共同指定, 文本描述了对查询图像的语义修改。
![[Pasted image 20260321212738.png]]
2.2 方法
2.2.1 总体思想：首先使用某个嵌入函数 f对候选图像库进行预索引（pre-indexing），然后将图像-文本查询表示映射到同一特征空间中，并利用该表示检索候选结果。
- r^t = f(I,"") --> pre-indexing
- r^q=f(Iq,T)  --> 该表示
	- f是嵌入函数
	- Iq是查询图像
	- T是相关文本
- 通过遍历计算r^t 与所有候选图像的 r^q 的cosine相似度来检索最可能的图片。 -->检索候选结果
2.2.2  ConText-CIR model的推理
- 问题：f是什么呢？即，推理阶段的模型是怎样的。
- ![[Pasted image 20260321214941.png]]
	- NP：noun phrases 名词短语
- 对查询，如何映射到特征空间：
	- 相关文本经过文本编码器，得到融合了上下文信息的文本特征
	- 查询图像经过图像编码器，得到图像特征
	- 将文本特征与图像特征输入交叉注意力模块，生成跨模态融合特征；
	- 跨模态融合特征通过注意力池化得到，最终的视觉语言特征r^q 
- 对候选图像库中的图片，如何映射到特征空间：
	- 把相关文本设置为“”即可,得到r^T 
- 查询：
	- 计算r^q 与各个图片的r^T 的cosine相似度，得到相似度最高的一个或几个作为结果
2.2.3 ConText-CIR model的训练 --> 损失函数的设计、和数据集的创新
文章的创新不在于模型的架构，而在于模型的训练。
2.2.3.1 现在的方法的局限性和处理方式
- 现有方法和数据集主要关注简单的文本修饰，这些修饰通常只是对前景目标进行直接、明显的修改，因此难以建模更长、更丰富的文本与图像之间的交互。
-  ![[Pasted image 20260321212738.png]]
	- 处理方式一：对训练集进行增强，让文本修饰更加丰富
	- 处理方式二：让文本中“名词短语的表示”更多地关注“查询图像中的相关区域”
	- ![[Pasted image 20260321224418.png]]
- ![[Pasted image 20260321224550.png]]
2.2.3.2 Loss 
- Text Concept-Consistency Loss：让文本中“名词短语的表示”更多地关注“查询图像中的相关区域”，对注意力模块进行的正则化
	- ![[Pasted image 20260321224724.png]]
		- T_NP_i：融合了上下文信息的名词短语的嵌入表示， 第i个。i-th noun-phrase in the context of the original text T
		- NP_i:  仅包含名词短语本身的嵌入表示，第i个。名词短语在单独输入文本编码器时所得到的表示。
	- 上下文交叉注意力图：这个文本嵌入，受到了其他概念属性的混淆，不能保证交叉注意力图在细粒度上对齐。但是融合了上下文信息的但是包含了上下文信息。
	- 独立交叉注意力图：仅包含概念本身的嵌入表示能够提升概念与图像之间的定位（grounding）效果，因为这类概念特定的嵌入不会受到其他概念属性的混淆，也不会被文本中的其他概念所抑制，从而实现更集中的定位。但是缺乏上下文的信息。
	- 作用效果：让名词短语的交叉注意力图在融合上下文的情况下，更多地关注“查询图像中的相关区域”。 \epsilon 提供了波动范围。
- 对比损失：从预测结果和目标结果的匹配程度来考虑的，主损失
	- ![[Pasted image 20260321232212.png|638]]
	- 细节：增加了Query Negative
- 总损失函数：
	- ![[Pasted image 20260321232329.png]]

2.2.3.2 自动数据生成流水线

- 用CIRR 生成了 CIRR_R数据集
- 自己生成了全新的数据集
3. 实验
- Aggregated = CIRR +  CIRR_R + LaSCo + Hotel-CIR 
![[Pasted image 20260321234825.png]]
- 上面的训练集包含了CIRR和CIRR_R，测试也包含了CIRR。由于是Zero-shot，所以只能选择LaSCo + Hotel-CIR 
![[Pasted image 20260321234933.png]]
- 数据集的消融实验
![[Pasted image 20260321235342.png]]
- 在没有增加图片的情况下，改变相关描述，就有很大的提升
- ![[Pasted image 20260321235523.png]]
- 定性结果
-  ![[Pasted image 20260321224550.png]]


训练
- CIRR
- LaSCo
- Hotel-CIR
- CIRR_R


总结：
- 提出了概念一致性损失
- 提出了自动数据生成流水线
- 在当前各项基准测试中达到了新的最优性能
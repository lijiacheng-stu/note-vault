先采用第一部分（4）约束对齐的算法，针对![](file:////Users/lijiacheng/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image002.png)得到通过四层校验的候选窗口。一个候选窗口包含了哪儿颗卫星在哪儿个时间段能针对哪儿个任务进行有效观测的信息。

对候选窗口![](file:////Users/lijiacheng/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image004.png)字段进行精细化，通过计算得到具体的覆盖区域的集合（这个集合的形式参考第一部分的空间约束![](file:////Users/lijiacheng/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image006.png)精准需求以确定性几何图形描述）。

对所有窗口的覆盖区域的集合求并集，判断是否包含![](file:////Users/lijiacheng/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image002.png)中的![](file:////Users/lijiacheng/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image009.png)，若包含，进入下一节内容，若不包含，则需要调整需求。


3.2.2 候选可行解的构建

这一节面向的是3.2.1中候选窗口集合能够提供的最大联合覆盖区域包含![](file:////Users/lijiacheng/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image002.png)的场景；

候选窗口集合的子集能够提供的最大联合覆盖区域也可能包含![](file:////Users/lijiacheng/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image002.png)。我们应该把能够提供的最大联合覆盖区域也可能包含![](file:////Users/lijiacheng/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image002.png)的最小子集作为候选可行解，因为不考虑与正在执行的任务所占用的窗口冲突的话，这些子集就能够提供满足T_rem的规划方案。这样的最小子集能够避免区域重复探测所产生的额外开销。
enum类型列表和方法怎么理解？
collect(Collectors.toList())怎么理解？


controller：
- 决定了model，以及使用model用于渲染的view
- model存在SessionAttribute，它是特殊的。在进入controller时，新建/读取相应的属性，在离开时，保存最新的属性值。且这部分，各个controller是共享的。

view:
- 能够访问到model，通过${}访问
- 能够


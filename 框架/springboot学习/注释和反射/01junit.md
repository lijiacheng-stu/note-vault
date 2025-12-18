- **作用：** 
junit可以用来对方法进行测试的框架，idea中集成了这个框架
#### 使用步骤
- 编写工具类StringUtil，在类中形成需要测试的方法lengthOfString(),maxIndex()
- 编写测试类StringUtilTest(注意类名命名规范)，和方法名testLengthOfString(),testMaxIndex()
此时的测试方法是公开，无参，无返回值
- 在方法上引入Test注解，并且引入Junit框架
- 在测试方法中，加入对应的测试用例，（输入，期望输出），通过断言及机制来让机器而非人工判断实际输出是否和希望输出相同
![[Pasted image 20250205170747.png]]
#### Junit中的其他注解
- Junit4中的注解
![[Pasted image 20250205170830.png]]
- Junit5
![[Pasted image 20250205170915.png]]

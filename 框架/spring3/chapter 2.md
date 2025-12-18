学习了向spring context 实例中加入bean的三种方法，分别是：
- @Bean annotation
步骤：
![[Pasted image 20250430223740.png]]
使用场景：只有当要加入context中的类在libs中，无法对类添加component注解的时候，才会使用
- stereotype annotations
步骤：
![[Pasted image 20250430223705.png]]
使用场景：只要能用，一定用这种方法。
- registerBean()
步骤：
![[Pasted image 20250430223901.png]]
使用场景：
![[Pasted image 20250430224121.png]]
在这个场景中，只要绿色的加入到context中。就可以配合逻辑语句，动态的调控了。
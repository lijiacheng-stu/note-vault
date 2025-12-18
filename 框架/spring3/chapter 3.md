介绍了三种将spring context中的beans关联起来，实现的是”have a“的关系（包括composition组合关系，aggregation聚合关系）的方法：
- 配置文件configration class中@Bean annotation标记的方法，通过在方法中引入参数，spring在context找到实例赋值给参数（推荐），或者有其他@bean方法在这个配置文件中的时候，可以通过调用方法
- 在定义对象的类中进行，通过@autowired
	- 属性 autowied
	- 构造器 autowield
	- setter方法 autowired
尽可能使用构造器autowield的，当类作为dependency中的类无法添加@autowired时，只能通过方法一；否则是构造器autowield。之所以不用属性 autowied，因为标注@autowired的属性无法被final修饰，因为类的对象构造出来后，再反射方法注入，此时由于final属性初始化时已经有了（必须有）对象，因此无法实现，因此有局限性。既然使用了方法二，那么肯定可以用@component的方法。使用配置的方法也是可以的。

1. python中的类和Java中的类的不同之处：
	- python中的属性是private和public，protected这样的权限修饰符的。（我们都是成年人是python的设计哲学）
	- java中属性统一给的，但是在python中式self.attribute_name = attribute_value给的，一般都在__init__中给定，但是也可以在任意函数中增加属性，这就是灵活性。
	- 在java中，子类继承父类，构造体一定要先运行父类的构造再运行子类的构造，当父类是默认的构造器时，会子类中会隐士调用。但是再python中，不显式调用就不执行
	- 在java中，一个文件中的public的类只能有一个，而在python中可以有多个。所以python把一个文件称作为模块，而不是文件。

 2. python中的类和Java中的类的相同之处：
	- 有print(obj)时调用__str__()，但是这个方法不是继承自obj，但是效果和toString()相同


3. 对import的理解：
	- python中import的是命名空间，每个模块命名空间是分立的，不会传递命名空间。这有点想C/C++中的声明，我声明有这个东西，但是这个东西是什么你别管。
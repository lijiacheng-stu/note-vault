

### 布局
#### 左侧
##### 左上
All Classes、All packages、All profiles(compact1 compact2 compact3) 、
##### 左下
Interfaces、Classes、Enums、Exceptions
斜体->interface

#### 右侧

### 常用类
#### Math
常用的常数和方法都是static类型的，意味者可以直接Math.method()使用
field 
E PI
method
abs max pow ceil floor random（[0.0,1)）

#### System

常用的常数和方法都是static类型的

System.currentTimeMills() 可以用以测试程序运行时间，单位是毫秒
时间原点：1970年1月1日 00:00:00 这个时间是格林尼治时间
东八区：1970年1月1日 08:00:00


![[Pasted image 20240325100557.png]]
exit()中的status的值非0都是非正常退出，底层调用的是Runtime中的exit()方法即
```java
public static void exit(int status){
	Runtime.getRuntime.exit(status);
}
```

#### Runtime
Runtime的方法几乎是动态的，也就是说调用这些方法得先产生对象。
如何产生对象呢？
Runtime的构造器是私有的，所以其他类不能直接new；
有一个属性currentRuntime=new Runtime(); 但是这个属性是私有的，是静态的，final的，所以不能修改，不能被其他类访问，但是随着类的加载就能够访问了。
有一个函数getRuntime()返回了currentRuntime();
这样的好处就是一个类只可能有一个对象。
![[Pasted image 20240325104402.png]]

#### Object
分析System.out.println();是怎么来？
- 在IDEA中输入System，进入这个类中
- 找到out这个属性，返回值是PrintStream，public static修饰可以直接访问，所以他是PrintStream的实例，可以调用其中的方法
- 查看PrintStream中方法println()的使用
- 问题：out默认初始化为Null，所以这个实例其实还不能调用方法，为什么还是调用了呢？
System.out.println(System.out);打印结果是java.io.PrintStream@10f87f48，说明System.out是被初始化的，什么时候被初始化的呢？？

如何理解String中的return this;的含义？
- 这个方法具有这样的结构
```java
class ClassType{
	public void ClassType methods(){
		renturn this;
	}
}
```
- 分析：this就是一个对象，return this; 则这个，return返回了ClassType的对象，所以函数的返回值必定得是这个类的类型，或者是它的父类
- `str.toString()` 调用的代码就是`return this;` 所以和调用前是完全一样的，冗余代码

如何理解Sysout.out.println(String x);打印的是x指向的字符串，而不是“包名@地址”？


toString() 包名@地址
equals(object o) 比较地址值是否相等，可能后面有些类被重写了，比如String；


#### BigInteger
常用的构造方法：
```java
public BigInteger(String val);
public static BigInteger valueof(long val);
```
计算：
由于BigInteger是属于类的，类的对象的+-* `/`  是不被允许的，都得调用方法
存储原理：
int signum->存储正负号
int[] mag->将字符串的正数部分，转成2进制数，32位为一组，转成int整数，放在int[] mag中

#### BigDecima
基本数据类型：boolean char 整形 浮点型
数字的存储情况
对于整数
byte 1B  shot 2B int 4B long 8B
有一个bit位表示符号，特别地1000 0000表示负数地最大值。位数是n，范围-2^(n-1)~2^(n-1)-1表示的是负数,-1到1有几个数字，3个不是2个
对于小数
float 4B 小数部分23bit
double 8B 小数部分52bit 
但是0.226，转成二级制数，55位，导致存储上精度的损失。
![[Pasted image 20240325165238.png]]
底层的存储原理
遍历字符串的每一个字符，并且存储在byte[] value

#### 时间
##### Date

#### 包装类
##### 概念
![[Pasted image 20240327214130.png]]
即：
![[Pasted image 20240327214204.png]]
**基本数据类型--对应包装类**
![[Pasted image 20240327214307.png]]
##### 如何产生对应的包装类呢？
- 自动装箱之产生对应的包装类
```java
Integer k=15;
method(18);
public void method(Object obj){…};
```
- 方法
```java
Integer k=Integer.valueOf(18); //-128~127指向预先生成的一个Integer数组中
//构造器的方法 即new的方法已经deprecated了
```
##### 包装类有哪儿写方法呢？
- 对于Integer
	-  自动拆箱之数字类型的计算
	```java
Integer in1=Integer.valueOf(18);
Integer in2=Integer.valueOf(36);
sout(in1>in2); //in1和in2转成18 36后进行计算
Integer in3=in1+in2; //先拆箱，再装箱
	```  
	- 整形转成其他进制:静态方法
	```java
public static String toBinary/Octal/HexString(int i);
	```
 
- 除了Character外都有`public static parseXxx(String s)`  方法,用以生成对应的基本数据类型
```java
int k=Integer.parseInt('18');
double d=Double.parseDouble('2.8');
```
##### 包装类在方法重载用的特点
```java
//情况1-->方法重载的时候，有限调用实参和形参类型一致的那个方法
class A{
	public void method(int i){sout("int打印");}
	public void method(Object obj){sout("Object打印");}
}
class B{
	psvm{
		method(18);//int打印
		method(Integer.valueOf(18)); //object打印
	}
}
//情况2-->自动拆箱
class A{
	public void method(int i){sout("int打印");}
}
class B{
	psvm{
		method(18);//int打印
		method(Integer.valueOf(18)); //int打印
	}
}
//情况3-->自动装箱
class A{
	public void method(Object obj){sout("Object打印");}
}
class B{
	psvm{
		method(18);//object打印
		method(Integer.valueOf(18)); //object打印
	}
}
```



#### Attays
##### `public static <T> void sort(T[] a, Comparator<? super T> c)`
**作用：** 这个方法非常重要，掌握了这个方法之后，能够对数组中为任意对象时，按照自己的心意进行排序。
**备注：** 第二个参数的赋值，引出了下面的lambda表达式
##### lambda表达式
###### 概念

![[Pasted image 20240329161858.png]]
细节：
- 函数式接口，用@FunctionalInterface进行检验，是只有一个抽象方法的接口
- lambda表达式，本质是生成匿名内部类（实际的类是具有继承或实现关系的，重写了父类或接口的方法）对象，是函数式编程的体现
###### 语法
- 判断接口是否为函数式接口-->@FunctionalInterface辅助判断，本质接口中只有一个抽象方法
- 判断目的是否是写匿名内部类
形式：
```java
CatIn ci=new CatIn(){
			@override
			public String method(String s){
				return "eat"+s;
			}
		}
```
本质：创建接口的实现类，并且对接口中的方法进行重写
- 对匿名内部类的写法进行优化
	- 只写重写的方法，只关注重写方法的参数和函数体，通过箭头连接` (String s)->{return "eat"+s;}`
	- 对表达式子进行进一步简化：可推导，可省略
		- 形参类型省略：因为原来的接口定义了参数类型，可以省略:改(String s)为(s)
		- 形参列表只有一个参数，省略()：改(s)为s
		- 函数体只有一行：
			- 有return，如果省略的话，必须同时省略{}，return,分号：改{return "eat"+s;}为“eat”+s
			- 如果没有return的话，省去{}和分号
最终形式变为：
`CatIn ci=s->"eat"+s;`
###### 实例
```java
public class Test{
	psvm{
		//匿名内部类写法
		CatIn ci=new CatIn(){
			@override
			public String method(String s){
				return "eat"+s;
			}
		}
		//lambda写法
		CatIn ci2=(String s)->{return "eat"+s;};
		//lambda简化写法
		CatIn ci3=(String s)->"eat"+s;
	}
}

@FunctionalInterface
interface catIn{
	public abstract String method(String s);
}
```





## Junit单元测试
### 测试的分类
![[Pasted image 20240408095026.png]]
- Junit就是**白盒测试**
### Junit的使用规范
![[Pasted image 20240408095154.png]]
![[Pasted image 20240408100734.png]]

## 反射
### 反射的地位和概念
![[Pasted image 20240408102353.png]]
### 获取Class对象的三种方式
![[Pasted image 20240408102442.png]]
![[Pasted image 20240408102551.png]]
预备知识：
- getClass()方式是Object中就定义的方法
结论：
- 字节码文件加载入内存的实际机制是：类加载器创建Class对象，并根据*.class 文件的情况对Class对象的Filed[] Contructor[] Method[]属性进行赋值
- 三种Class对象的获取方式对应于Java代码在计算机中经历的三种方法
- 三种获得Class对象的方法都会引起类加载器对字节码文件的加载，但是只会加载一次，不论通过哪儿中方式获得的类对象其实都是同一个
### 利用Class对象获取方法构造器属性并使用
#### 获取类的属性、方法、构造方法、类名
![[Pasted image 20240408111045.png]]
**对获取构造/成员方法们时，参数列表的解释** 
- 方法有三要素：方法名，参数列表，返回值列表
- 确定一个方法有两个参数：方法名，参数列表。相同方法名、不同参数列表的方法构成方法的重载
#### Field Method Constructor类的常用方法
##### Field
获得Filed的一个属性之后，目的无疑就是获取值和设置值，涉及到set和get方法。由于Field属性是对于类而言的，属性的值是对于对象而言的，那么如果单纯的对Field的对象获取值是没有意义的，一定得表明具体的对象。
对于private修饰的成员变量，不能直接方法，必须先忽略访问权限修饰符的安全检查，得使用setAccessible(true)，进行暴力反射
![[Pasted image 20240408105558.png]]
##### Constructor
获取构造方法的目的，就是创建对象。
对于private修饰的构造方法也是可以setAccessible的
![[Pasted image 20240408110903.png]]
##### Method
获取方法的目的，就是调用方法。方法调用的单位是对象，所以得指定对象。也存在private修饰问题，直接暴力反射
![[Pasted image 20240408111745.png]]


## 注解

### JDK中预定义的一些注解
![[Pasted image 20240408150110.png]]

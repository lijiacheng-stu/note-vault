## 修饰符
访问权限 存储 返回值 函数名 参数列表 函数体
#### final
![[Pasted image 20240317165526.png]]
![[Pasted image 20240317170133.png]]
核心：与变量绑定的内容是不可变的，对于基本数据类型，这个内容就是数据值，对于引用数据类型，这个值就是地址值
#### 权限修饰符
四个位置：本类 本包 其他包中的子类 其他包中的其他类 （不存在单纯的只有子类能用）
![[Pasted image 20240317171355.png]]
#### static：属于类而非具体的对象，具有不依赖于对象的特点，是一种存储特点
##### 对变量的修饰
随着类的加载，而加载进入堆中的静态存储区，使之优先于对象的而可以进行访问。
![[Pasted image 20240316141201.png]]
##### 方法的修饰
##### 工具类：static方法的应用案例
随着类的加载，视频里好像是方法区，反正都是理论模型，我姑且认为是静态存储区吧。相当于在堆中有个区域叫静态存储区，在静态存储区有许多区域，每个区域都有对应的类。通过类的名字来找到对应的区域的位置。
![[Pasted image 20240316132129.png]]

![[Pasted image 20240316132043.png]]
![[Pasted image 20240316135754.png]]
要点：静态方法不依赖于对象执行，它和类的加载同时加载。
推理：
- 静态方法不能访问没有被static修饰的变量和方法
对没有被static变量而言，它的作用是反应对象状态的，只有对象创建后才具有意义，换句话说，在没创建之前，不能被使用。 如果静态方法能够方位这些变量，那么必然要在对象创建之后，这与静态方法不利待遇对象执行相矛盾。
对于没有被static修饰的方法：这些方法没有对变量的访问进行限制，也就是可能访问到没有被static修饰的变量，由上条解释可知，访问这些变量是不被允许的，所以不能访问。
- 非静态方法可以访问所有
非静态方法的调用必然产生于对象产生后，这时，静态变量、静态方法，成员变量和一般的方法都已经存在，自然可以访问。
- 静态方法种没有this关键字
在JVM中，public study(Student this){} 这个Student this是隐含不写的，this赋值的是对象的地址值。既然不依赖于对象自然就没有this啦。

## 继承
#### 概念
![[Pasted image 20240316181051.png]]
![[Pasted image 20240316182512.png]]
#### 继承的特点
![[Pasted image 20240316203239.png]]
**只支持单继承，不支持多继承**：一个类只有一个父类，不能有多个
**支持多层继承** ：父类也可以有父类，这时候，是子类的间接父类
注：将会形成一个树状的结构

#### 子类能继承父类中的哪儿些内容
- 一个类的包含的成分
构造方法、成员变量、成员方法
- 对于构造方法： 非私有 不能 | private 不能
一个类的构造方法这样的要求，没有返回值类型，构造方法的名称必须和类名相同。
如果说继承了构造方法，那么子类中就不用写构造方法了，那么子类的构造方法就违反了构造方法中构造方法的名称必须和类名相同的要求。
- 对于成员变量：非私有 能 | private 能
子类继承了带了”锁“的private的变量，不能直接使用，如果要使用，得用set和get方法
- 队员成员方法： 非私有 能 | private 不能
虚方法表：方法+地址（方法非static 非final 非private修饰）
更新并维持虚方法表：字节码文件进入方法区的同时，更新并维持虚方法表：继承父类的虚方法表，添加自身虚方法
对象访问方法：第一步，根据对象变量保存的地址，找到堆中实际数据，根据实际数据中保存的字节码的地址，找到方法区中的字节码；第二步，在虚方法表中寻找，如果找到此方法，则根据方法对应的地址找到对应的字节码（可能在父类中，或间接父类，或者自己身上），则将此方法的字节码加载到方法区中；如果说，虚方法表中没有找到此方法，则在自己的字节码中寻找（此时的有final static private进行修饰），如果找到则载入方法区，如果没找到，则转向父类，如果找到的非private修饰的，则载入方法区，否则不载入，报错。


#### 访问特点:类中的方法对于成员变量和成员方法的访问特点
**对于成员变量：**
不特别说明时：先从局部位置找，本类成员位置找，父类成员位置找，逐级往上
可以更改起始查找的位置，name从局部位置开始，this.name从成员位置开始，super.name从父类位置开始
**对于成员方法：**
默认时，从子类的虚方法表中开始查找，即eat()等价于this.eat()，因为它的父类也维持了一个虚方法表，可以调用父类的虚方法表，super.eat(); 
对虚方法表的再认识：从方法名的角度来讲子类确实包含了父类，但是从方法对应的功能来讲，由于重写的存在，所以父类的虚方法表还是有不一样的。

**方法的重写：**
![[Pasted image 20240316220645.png]]
![[Pasted image 20240316221802.png]]
#### 继承的特点
![[Pasted image 20240316222120.png]]
![[Pasted image 20240316222152.png]]
this(……)用于有默认值的空参构造

## 多态
#### 概念
![[Pasted image 20240317143654.png]]

![[Pasted image 20240317160938.png]]


## 包
![[Pasted image 20240317165425.png]]


## 代码块
**局部代码块**（淘汰了）
![[Pasted image 20240317173557.png]]
作用：提前结束变量的声明周期

**构造方法块**
![[Pasted image 20240317174005.png]]
缺点：不够灵活，多个构造方法时，若不想执行构造代码块中的内容是做不到的
其他平替方案
![[Pasted image 20240317174357.png]]
**静态代码块**
![[Pasted image 20240317174459.png]]
## 抽象类抽象方法
![[Pasted image 20240317183835.png]]
抽象类是不能产生实例的。

## 接口
![[Pasted image 20240317185618.png]]
![[Pasted image 20240317190344.png]]
**定义接口和使用**
![[Pasted image 20240317190517.png]]![[Pasted image 20240318101458.png]] 
**接口内的方法**
（默认） public abstract 类型 method();
默认方法 public default 类型 method(){方法体};  //实现接口升级，提高兼容性，可以被重写，实现类对象调用
静态方法 public static 类型 method(){方法体}; //用接口名.方法名 进行调用
私有方法 
private default 类型 method(){方法体}; //为public default 类型 method(){方法体}; 为类内部函数服务，提高代码复用性
private static 类型 method(){方法体}; //为public static 类型 method(){方法题};为类内部函数 服务，也是提高代码复用性，由于静态方法只能调用静态方法。
**接口与类之间的关系**
![[Pasted image 20240318110244.png]]


**适配器类**
![[Pasted image 20240318123055.png]]
## 内部类
![[Pasted image 20240318190028.png]]
#### 匿名内部类
**格式**
```java
new 接口名/类名 ( , ){
	方法的重载
};

//区分
new 类名();
```
这段代码的本质：生成匿名内部类的对象
**原理**
- 生成类的字节码文件：在A类，执行了上面的代码后，系统会产生这样的一个类，类名是“调用者的类名$数字”，这个类继承/实现了类/接口，同时有进行方法的重载。可以说是一个全新的类了，这个类是调用者的内部类。
- A类中产生匿名内部类的对象：A类产生了“调用者的类名$数字”的对象，由于这个匿名内部类是没有对象的，所以如果要用变量来指代的话必须得用以下格式。对方法的调用，符合左边编译又执行的。
```java
接口名 name=new 接口名/类名 ( , ){
	方法的重载
};

类名 name=new 接口名/类名 ( , ){
	方法的重载
};
```
- 其他
{}内部的是类的本尊，接口名和类名表示本尊继承或实现的类或接口。
**应用场景：**
需要新的类，而且这个类是其他类的子类或实现类，但是**只使用一次**，不需要创建新的类，使用匿名内部类
具体：
方法的参数是接口或者类时。


## 正则表达式
作用：
![[Pasted image 20240325170229.png]]
在pattern类介绍了对应的规则，在public boolean matches(String regex) ;中使用
![[Pasted image 20240325172459.png]]
（？i）忽略大小写
## 集合
### 体系结构
集合只能存储对象，有了包装类的用武之地了。Vector已经被淘汰了。
![[Pasted image 20240327170922.png]]
（红颜色表示接口）

![[Pasted image 20240327161436.png]]
![[Pasted image 20240330223828.png]]
### 数据结构
#### 栈
特点：后进先出
操作：进栈、出栈
应用场景：栈内存
![[Pasted image 20240329175548.png]]
#### 队列
特点：先进先出
操作：出队列，入队列
![[Pasted image 20240329175604.png]]
#### 数组
特点：存储相同的数据类型，连续的内存空间，查询快，增删慢
![[Pasted image 20240329175858.png]]

#### 链表
特点：存储相同的数据类型，存储离散，查询慢，增删快
![[Pasted image 20240329180249.png]]

#### 树
##### 概念
演变：节点->二叉树->二叉排序树->平衡二叉树
- 节点 父节点 作子节点 右子节点
- 度：每个节点的子节点数量，度小于等于2就是二叉树
![[Pasted image 20240330094917.png]]
![[Pasted image 20240330094941.png]]
- 二叉排序树：任意左子树上的节点小于当前节点，任意右子树上的值大于当前节点
- 平衡二叉树：任意节点左右子树高度差不超过1
##### 操作
- 查找:基于二叉排序树
	- 普通二叉排序树的弊端：添加节点时左右子树可能会高度差大，导致查询效率低-->平衡二叉树
- 遍历：前序遍历（当前节点，左子树，右子树），中序遍历，后序遍历，层序遍历
##### 平衡二叉树的旋转机制
###### 基础之第一步：公共步骤
从插入节点开始网上找，找到第一个不满足的父节点
###### 基础之左旋
旋转前：
![[Pasted image 20240330101518.png]]
旋转后
![[Pasted image 20240330101455.png]]

###### 基础之右旋
旋转前
![[Pasted image 20240330101918.png]]
旋转后
![[Pasted image 20240330101940.png]]


###### 应用之
四种情况
**判断情况的方法：**
1、先通过公共步骤，找到不平衡的点作为根节点
2、判断出插入的节点的位置：
	a、在根节点的左/右子树 ，不妨设左子树-->第一个左右
	b、判断节点在左子树的左子树还是右子树-->第二个左右
**四种情况** 
- 左左
操作：一次右旋
- 右右
操作：一次左旋
- 左右
操作：先局部左旋，再整体右旋
分析：第一步局部左旋的意义在于将“左右”-->"左左"
局部左旋：以根节点的左孩子节点作为旋转时的根节点，进行左旋操作
- 右左
操作：先局部右旋，再整体左旋

##### 红黑树

![[Pasted image 20240330110146.png]]
![[Pasted image 20240330110210.png]]
![[Pasted image 20240330110247.png]]


### 泛型
#### 概念
##### 为什么要引入泛型？
##### 泛型的细节
- 只支持引用数据类型
理由：一开始的集合什么都能存，为object类型， 所以数字这种基本数据类型就得转成对应的包装类。
- 在不对泛型指定类型，默认将E赋值为Object类，可以对变量进行任何对象的赋值，多态。
评估：这个就是JDK5之前的形式。 不能使用子类的特有方法，否则得强转。
- 检验语法正确提前到了编译时期，避免强制类型转换可能出现的异常
- 伪泛型
#### 泛型的使用
##### 泛型类
![[Pasted image 20240330084545.png]]
E：element   K：key  V：value  T：type
##### 泛型方法
![[Pasted image 20240330084914.png]]
![[Pasted image 20240330085000.png]]

##### 泛型接口
![[Pasted image 20240330085654.png]]
```java
//方式一:实现类给出泛型的类型
public class demo implements List<String>{}
//方式二：实现类延续泛型，创建对象是再确定
public class demo<E> implements List<E>{}
```

#### 通配符与继承
##### 通配符
- `?` 代表一切类型
- `? extend A` 传递A和A的子类
- `? super A` 传递A 和A 的父类
##### 泛型不具备继承性，但是数据具备继承性
###### 概述
给 `ArrayList<Ye>` 型的变量赋值，只能传`Arraylist/子类<Ye>` 型的变量；
给 `ArrayList<Ye>` 型的变量添加数据，能够传Ye的子类
###### 泛型不具备继承性
对于泛型类来讲，如`ArrayList<E>`涉及了两个类，第一个类反映了对象本身的身份Arraylist，
第二个类反映了对象中某些属性或者方法的数据类型E。
对于一个方法如以下，参数需要的数据类型是``ArrayList<Ye>``,根据两类理论，实参中第一个类是ArrayList第二个类是与Ye之间具备继承关系Zi ->Fu ->Ye, 由于不具备继承关系，后两种不能传，只能传第一种。
如果改进测试方法，两类理论中，第一个类具备继承关系呢？
可以继承，但是泛型必须类型必须得完全一致。
总之，主类型可以具备继承关系，（次类型）泛型一定得同一
```java
//测试1：两类理论中，第一个类相同，第二个类具备继承关系-->不能多态，即泛型不具备继承性：
public class Student {  
    public static void main(String[] args) {  
        ArrayList<Ye> list1=new ArrayList<>();  
        ArrayList<Fu> list2=new ArrayList<>();  
        ArrayList<Zi> list3=new ArrayList<>();  
        method(list1);  
        method(list2);  //报错 提供ArrayList<Fu> ，需要ArrayList<Ye>
        method(list3);  //报错 提供ArrayList<Zi> ，需要ArrayList<Ye>
    }  
    public static void method(ArrayList<Ye> list){  
  
    }  
}  
class Ye{}  
class Fu extends Ye{}  
class Zi extends Fu{}
```
```java
//测试2：两类理论中，第一个类具备继承性，第二个类有些与形参相同，有些与形参不同
public class Student {  
    public static void main(String[] args) {  
       Ye<String> y=new Ye<>();  
       Fu<Integer> f=new Fu<>();  
       Zi z=new Zi();  
       method(y);  
       method(f); //报错，需要Ye<String> 提供Fu<Iteger> 
       method(z);  //正常
    }  
    public static <E> void method(Ye<String> list){  
  
    }  
}  
class Ye<E>{}  
class Fu<E> extends Ye<E>{}  
class Zi extends Fu<String>{}
```
###### 数据具备继承性
向`ArrayList<Ye> list`  可以添加Ye以及其子类的对象 
```java
public class Student {  
    public static void main(String[] args) {  
        ArrayList<Ye> list=new ArrayList<>();  
        list.add(new Fu());  
        list.add(new Zi());  
    }  
}  
class Ye{}  
class Fu extends Ye{}  
class Zi extends Fu{}
```
### Collection
#### Collection独有的方法 
![[Pasted image 20240327171141.png]]
注意：
- add方法的返回值true false，对于List来讲没什么用因为无论增加什么都会加进去为true，但是对于Set来讲有用，集合中已经存在的不会再加入true 和false
#### collection的实现类对象进行遍历
##### 方法一：迭代器iterator
**对象的获取** 
因为iterator是一个接口，所以他没有构造器。collection它也是接口，没有构造器，而且collection也是不iterator的实现类（如下可以说明）。怎样创建iterator对象呢？
```java
public interface Collection<E>
extends [Iterable](../../java/lang/Iterable.html "interface in java.lang")<E>
```
- 对于collection，通过多态的方法产生"collection对象" coll：
`Collection<String> coll=new ArrayList<>();`
分析：由于ArrayList是collection的实现类，根据“左编译，右运行”的原则，那么coll对象能够调用collection类中的所有方法，而这些方法已经被ArrayList重写了。
- 对coll调用方法iterator(),产生的Iterator对象通过it接收：
`Iterator<String> it=coll.iterator();`
分析：iterator(),肯定会在ArrayList中重写，并且返回Iterator型对象。
问题：Iterator是一个接口，具体的方法implements肯定是基于一个实现类的，也就是ArrayList中重写的返回的Iterator对象，肯定不是Iterator类，而是Iterator的实现类。在ArrayList中制作了这个实现类Itr，里面重写了remove,next,hasNext等方法。


**迭代器的方法**
![[Pasted image 20240327172906.png]]
default void remove()
个人理解：
如果collection的索引是从0开始的，那么迭代器的指针就是从-1开始，hasNext()表示-1+1后确定是否具有元素，next()获取指针下一个的元素

**细节** 
![[Pasted image 20240327173234.png]]
- 1中，当迭代器已经是最后一个，再使用next()便会抛出NoSuchElementException
- 3中，不是说用了就会报错，就是最好和hasNext()配套使用
- 4中， 如果用集合的方法删除，会抛出异常，如果要删除，要使用迭代器中的remove()

##### 方法二：增强for
![[Pasted image 20240327195713.png]]
注意：
- 这个for中的变量名是第三方变量，修改第三方变量的值不会改变原来的数据


##### 方法三：lambda表达式


#### List
##### list的特点和独有方法
![[Pasted image 20240327200658.png]]
![[Pasted image 20240327200715.png]]



##### ArrayList
底层是数组
##### LinkedList
底层是带头尾指针的双联链表-->头尾部插入比较快，有专门头尾插入的方法

#### Set
##### Set的特点和特有方法
![[Pasted image 20240330111559.png]]
**遍历** 由于是无序的所以不能使用索引
迭代器 增强for  lambda表达式 （普通for和ListIterator就不行）
**方法** 基本上继承自collection
![[Pasted image 20240330114139.png]]




### Map
#### Map特有
##### 特点与方法
![[Pasted image 20240330202624.png]]
![[Pasted image 20240330202907.png]]
![[Pasted image 20240330205005.png]]
![[Pasted image 20240330205154.png]]
方法的注意事项：
- 对于put(),放入已存在的键，返回被覆盖的值；放入不存在的键，返回null
- 对于get(Object key),根据键返回值
- 对于keySet(),非常关键，是遍历Map的有利工具
##### 遍历方式
###### 键找值
**原理：** 
- 第一步，通过map.keySet() 得到key的集合
- 第二步，通过forEach()的lambda表达式，或者迭代器，或者增强for来遍历key
- 第三步，通过get(Object key)方法，根据键找值

###### 键值对对象
**原理：**
- 第一步,通过map.entrySet()得到entry集合
- 第二步，通过forEach()的lambda表达式，或者迭代器，或者增强for 来遍历entry
- 第三步，通过entry中的getKey()和getValue()方法来进行遍历
注意：
- Entry是Map的内部接口
- getKey()是抽象方法，所以执行的是哪儿个实现类的方法呢？

###### lambda表达式
**原理：** 
- forEach()

#### HashMap
##### 特点
注意：重点还是回去看一下HashSet的知识，区别就是这个时候存的是Entry对象，Hash值的计算只跟键有关，遇到相同的采取的是覆盖策略。 
![[Pasted image 20240330224341.png]]
![[Pasted image 20240330224550.png]]



#### LinkedHashMap
注意：仍然参考LinkedHashSet,hashCode用来找存储的未知，equals用来确定要不要存/覆盖，在Set中，相等就不存，Map中时相同就覆盖。
![[Pasted image 20240330225739.png]]
#### TreeMap
![[Pasted image 20240331090444.png]]

### Collections
常用的方法
![[Pasted image 20240331114444.png]]
### 不可变集合
**对List**
![[Pasted image 20240401085022.png]]
List.of()对元素数量没有限制

**对Set**
![[Pasted image 20240401090034.png]]
Set.of()对数量没有限制

**对Map**
![[Pasted image 20240401090205.png]]
- Map.of()对Map有数量限制，最多10对
![[Pasted image 20240401090237.png]]
- 当数量大于10对时候，使用Map.ofEntries()，如下
```java

```
- 终极方法 
![[Pasted image 20240401091611.png]]
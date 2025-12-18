### 可变参数
![[Pasted image 20240331113853.png]]
对注意事项的解释
- 若形参列表中可变参数有多个，那么无法确定实参列表中的哪儿些属于第一个，哪儿些属于第二个形参，如下：
```java
psvm{
	method(1,2,3,4,5,6,7)
}
public void method(int...a,int...b){……};
```
- 若可变参数不放在最后，那么将会可变参数会将后面的也认为是可变参数的内容
存在个问题：
可变参数本质是一个数组，那么传入一个数组的情况下，那什么时候数组只是作为一个元素呢？
![[Pasted image 20240401093828.png]]
跟泛型有关系吗？


### Stream流
#### 概念、思想、步骤
![[Pasted image 20240401102059.png]]
![[Pasted image 20240401091902.png]]
#### 步骤一：获得Stream流
![[Pasted image 20240401092851.png]]
- 对于单列集合：调用Collection中的方法
![[Pasted image 20240401092312.png]]
- 对于数组：调用Arrays中的方法
![[Pasted image 20240401092518.png]]
- 对于零散的数据
![[Pasted image 20240401092652.png]]
- 对于双列集合
双列集合->keySet,valueSet,entrySet方法转成单列集合



#### 步骤二：中间方法：通过观察返回值是否为Stream判断
![[Pasted image 20240401094113.png]]
 - filter方法，匿名内部类重写方法的返回值，true留下，false去除
 - skip和limit配合使用，截取一个流的一部分
 - distinct，依赖HashSet实现，所以依赖hashSet方法和equals方法，如果属性的话，得重写
 - map方法
 ![[Pasted image 20240401095715.png]]

#### 步骤三：终结方法
![[Pasted image 20240401095826.png]]
- collect方法
参数配合Collectors.toList() Collectors.toSet() Collectors.toMap() 

### 方法引用
#### 概念
![[Pasted image 20240401111154.png]]
3中介绍的就是使用的前提：
- 对方法：形参和返回值类型相同
- 对method(需要方法引用的参数1，…,参数n) ：参数一的类型得是函数式接口

![[Pasted image 20240401164028.png]]
![[Pasted image 20240401164042.png]]

### 异常
#### 体系结构
##### 体系
![[Pasted image 20240401170813.png]]

##### 顶级父类Throwable中常见的方法
![[Pasted image 20240401183456.png]]
![[Pasted image 20240401183522.png]]
![[Pasted image 20240401183350.png]]
- printStackTrace()最常用，包含了toString()和getMessage()中的内容，既能够展示错误，有能利用try……catch机制避免停止运行程序
#### Error
![[Pasted image 20240401171004.png]]
#### Exception
##### 基本概念
###### 结构

![[Pasted image 20240401170932.png]]

###### 运行时异常与编译时异常的区别
![[Pasted image 20240401172007.png]]
###### 异常的作用
![[Pasted image 20240401173034.png]]


###### 常见的异常
- ArrayIndexOutOfBoundsException 数组越界异常 如：
```JAVA
int[] arr={1,2,3};
sout(arr[3]);
```
- ArithmeticException 算数异常
`int k=3/0;`
- NullPointerException 空指针异常
```java
Student st=null;
st.toString();
```
##### 异常处理方式
###### JVM默认的处理方式
![[Pasted image 20240401173859.png]]
换言之：
- 没出现异常之前的代码都会被执行
- 异常后，输出异常的格式：
异常名称：异常原因
	异常位置
从下往上看。
###### 自己处理（捕获异常）
![[Pasted image 20240401175049.png]]
**四种情况的简略版本：**
![[Pasted image 20240401182648.png]]
**四种情况的详解版本：** 
![[Pasted image 20240401175146.png]]
**情况一： 如果try中没有遇到问题，怎么执行？** 
答：会把try里面的代码执行完毕，不会执行catch里面的代码
**情况二：如果try中可能会遇到多个问题，怎么执行？** 
答：
- 书写：会写多个catch与之对应
- 执行：try中遇到问题后，会跳转到一个第一个与此问题匹配的catch语句，执行，然后不再执行try语句，执行try……catch体系下方的代码。
- 扩展与细节：父类异常得写在下面，否则报错；多个异常执行的是相同代码是，异常类型可以用单竖线隔开
 ![[Pasted image 20240401181719.png]]
 **情况三：try中遇到的问题没有被捕获，怎么执行？**
答: try…catch白写了，最终会交给虚拟机处理
**情况四：如果try中遇到的问题，那么下面的其他代码还会执行吗？**
答：不执行了，直接转到catch当中，执行catch里面的与语句体

完整体系
try{}catch{}finally{}
- finally中的代码一定会被执行
###### 抛出异常
![[Pasted image 20240401190539.png]]
运行机制：
- 抛出异常给调用者，如果调用者在try……catch体系中，就能够捕捉到对应的异常了，继而执行catch下方的代码。
- throw抛出的是一个对象




###### 抛出异常和捕获异常的意义和使用场景
抛出：告诉调用者出错了
捕获：不让程序停止



##### 自定义异常类型
![[Pasted image 20240401192743.png]]
目的：获得这个异常的名字
例如：
![[Pasted image 20240401192922.png]]

### File
#### 概念
![[Pasted image 20240402100243.png]]
在文件层面对文件进行操作，但是不能读取文件的内容
#### 方法
##### 判断和获取
![[Pasted image 20240402163408.png]]
**细节与注意：**
- length()只能返回文件的大小，但是对于文件夹不行（不能正确反映），不存在则为0
- isDiretory存在且为文件夹就是true，否则为false，isFile同理
- 相对路径，将对于项目名称，从项目名称开始写，前面不写\
##### 创建与删除
![[Pasted image 20240402171819.png]]
- createNewFile()细节
![[Pasted image 20240402171908.png]]
- mkdir()细节
![[Pasted image 20240402172450.png]]
- mkdirs()细节
![[Pasted image 20240402172520.png]]
- delete()细节
![[Pasted image 20240402172641.png]]

##### 获取并遍历
![[Pasted image 20240402173002.png]]

### IO流
#### 概念
![[Pasted image 20240402210037.png]]
![[Pasted image 20240402210629.png]]
原则：
- 随用随开启，随不用随时关闭
- 高级流得关联基本流？
#### 体系结构
![[Pasted image 20240404124148.png]]
基本流：FileInputStream，FileOutputStream，FileReader，FileWriter
缓冲流：BufferedInputStream，BufferedOutputStream,BufferedReader,BufferedWriter
转换流：InputStreamReader,OutputStreamWriter
- **InputStream 抽象类** 
常用构造器：（空）
实现类对它的扩充：构造器：
核心：public FileInputStream(File) 
其他：public FileInputStream(String) //本质调用的是第一个方法
常用方法：
publcc abstract int read();
public int read(byte[]){}
public void close(){}

- Reader 抽象类
常用的构造器：

常用的方法：
public int read(){}
public int read(char[]){}
public abstract void close(){}

#### 字节流：OutputStream
##### FileOutputStream
###### 基本步骤及其细节 
![[Pasted image 20240402212851.png]]
###### 写数据的三种方式
![[Pasted image 20240402213237.png]]

当要向指定文本中写入字符串时，配合String下的`public byte[] getBytes()` 将对应字符串转成对应的byte数组。
- getBytes()会因为编码规则不同产生不同的byte[]，默认是UTF-8
![[Pasted image 20240403114814.png]]
对于byte[]，也可以转成相应字符串，也可以指定对应的解码规则，注意这里是在构造器中
![[Pasted image 20240403115032.png]]


###### 换行与续写
**预备知识：换行符**
换行就是写入换行符
![[Pasted image 20240402214011.png]]
**续写：构造对象时，第二个参数传true，打开续写开关**
![[Pasted image 20240402214559.png]]






#### 字节流：InputStream
##### FileInputStream
**基本步骤与细节** 
![[Pasted image 20240402215447.png]]
- 读方法时 `public int read()` :返回指针所对应字符在ASCII码上的数字，每调用一次，移动一次指针，读取到文件末尾了，read方法返回-1
```java
//字节输入流的循环读取
//设 a.txt中有文字 abcdefg
public class IoTest1 {  
    public static void main(String[] args) throws IOException {  
        FileInputStream fis=new FileInputStream("C:\\Users\\李嘉成\\Desktop\\javaStudy\\basic-code\\test\\aaa\\a.txt");  
        int b;  
        while((b=fis.read())!=-1){  
            System.out.print((char)b);  //abcdefg
        }  
    }  
}
```

##### 关键方法
###### read的两种方法
**数据为read返回值**
![[Pasted image 20240402224241.png]]
**数据读入数组** 
![[Pasted image 20240402224135.png]]
#### 字符流

#### 字符流：Reader
##### FileReader

reader方法的底层原理
![[Pasted image 20240403153147.png]]
#### 字符流：Writer
##### FileWriter
###### 构造方法
![[Pasted image 20240403151217.png]]

#### 缓冲流
- 在基本流地基础上，在内存中开辟了一个缓冲区，提高了读取速度，由于字符流的基本流本身就已经有了缓冲区，所以对速度的提升比较有限
- 关闭缓冲流时，构造时传入的基本流也会被关闭
- 字符流中的缓冲流相对于字符流中的基本流的优势在于有新的方法。readLine()，newLine() //readLine是对于BufferedReader而言的，不读取换行符号的。 newLine()是对于BufferedWriter而言的，提高平台兼容性（由于不同平台对换行的符号定义不同）
![[Pasted image 20240403165438.png]]
![[Pasted image 20240404102033.png]]
![[Pasted image 20240404103040.png]]
![[Pasted image 20240404103120.png]]
![[Pasted image 20240404104116.png]]
#### 转换流
![[Pasted image 20240404132609.png]]
#### 字节流：序列化流，反序列化流
##### 序列化流
###### 概念
又称对象操作输出流
作用：以一种人读不懂的形式吧java中的对象写到本地文件中
###### 构造与方法
![[Pasted image 20240405152906.png]]
注意：
- obj能被写入的前提是object这个类得实现标记型接口Serializable（没有方法的接口）
- writeObject写入时，不仅写入了对象信息，还写入了序列号
- 默认的序列号是根据当前Object中成员方法，成员变量等一切信息计算出来的，当原来的Object因为业务需求发生变化时，序列号将会发生改变，可以理解为版本号
- 当读取文件里的obj时，会比较文件中的序列号和现在类的序列号， 不匹配时将会报错。解决方法是固定版本号。
- 有些成员变量不想序列号到到文件中，此时这个变量用transient修饰，瞬态关键词，尽管写入的时候，瞬态变量被赋值了，但是读取的时候，对应的值是null
- 序列化流写到的文件中的数据不能修改，一旦修改，无法再次读取，报错，破坏原数据
##### 反序列化流
又称，对象操作输入流
![[Pasted image 20240406092104.png]]
##### 固定版本号的方法
**方法一：手动书写**
`private static final long serialVersionUID=1L` 
- 书写麻烦
- serialVersionUID赋值不规范
**方法二：setting中设置自动生成**
![[Pasted image 20240406093352.png]]
##### 对多个序列化流对象的读写
**幼稚做法**
写的时候，写多个；读的时候，读多个
弊端：写了3个读4次将会抛出EOFException
**标准做法**
写的时候，先把多个对象写入到集合中，读的时候，赋值给集合，再从集合中提取数据
- 写
```java
public class SerialTestOutput {  
    public static void main(String[] args) throws IOException {  
        Student s1 = new Student("zhangsan",23,"南京");  
        Student s2=new Student("lisi",24,"北京");  
        Student s3=new Student("wanhwu",25,"上海");  
        ArrayList<Student> list=new ArrayList<>();  
        list.add(s1);  
        list.add(s2);  
        list.add(s3);  
        ObjectOutputStream oos=new ObjectOutputStream(new FileOutputStream("C:\\Users\\李嘉成\\Desktop\\javaStudy\\basic-code\\iomodule\\files\\a.txt"));  
        oos.writeObject(list);  
        oos.close();  
    }  
}
```
- 读
```java
  
public class SerialTestInput {  
    public static void main(String[] args) throws IOException, ClassNotFoundException {  
        ObjectInputStream ois=new ObjectInputStream(new FileInputStream("C:\\Users\\李嘉成\\Desktop\\javaStudy\\basic-code\\iomodule\\files\\a.txt"));  
        ArrayList<Student> list = (ArrayList<Student>) ois.readObject();  
        for (Student student : list) {  
            System.out.println(student);  
        }  
  
    }  
}
```
**疑问/注意点**
- 因为写入的对象是ArrayList对象，是不是意味着Student就可以不实现implement了呢？
错。报NotSerializableException
- 已经写入Student对象于文件后，如果删除Student的实现Serializable接口，将会出现异常

#### 打印流：字节打印流，字符打印流
##### 体系
![[Pasted image 20240406100640.png]]
![[Pasted image 20240406101554.png]]
##### 字节打印流
**构造方法** 
![[Pasted image 20240406101606.png]]
**方法**
![[Pasted image 20240406102748.png]]
- 字节流没有缓冲区， printf和print区别在于字符串是不是格式字符串
##### 字符打印流
**构造方法** 
![[Pasted image 20240406102906.png]]
**成员方法**
![[Pasted image 20240406102928.png]]
- 和字节打印流的区别仅仅是有没有缓冲区的差别
- 缓冲区：将要打印的字符先寄存到缓冲区中，被动刷新：当关闭打印流或者缓冲区满时刷新缓冲区，将缓冲区中的数据写入。 主动刷新：在构造时增加autofush参数为true，以print语句为单位刷新


##### 根据打印流的知识解析System.out.println()
- System.out 是定义在System类下的成员变量
`public static final PrintStream out = null;`
- System.out在虚拟机启动的时候，由虚拟机创建，默认指向控制台，叫标准输出流，无法关闭
```java
psvm{
	PrintStream ps=System.out;
	ps.println("123");// 123
	ps.close();//试图关闭System.out
	ps.printlb("123"); //123 关闭失败
}
```
- Syetem.out调用了println方法
#### 压缩流//暂时不学
##### 体系
![[Pasted image 20240406105119.png]]

#### 基于IO实现的功能
##### 赋值粘贴文件
###### 通过FileInputStream和FileOutputStream实现
![[Pasted image 20240402222351.png]]
**read一个一个字节地读** 
```java
public class IoTest2 {  
    public static void main(String[] args) throws IOException {  
        long start = System.currentTimeMillis();  
        FileInputStream fis=new FileInputStream("C:\\Users\\李嘉成\\Desktop\\javaStudy\\basic-code\\test\\aaa\\bbb\\meeting_01.mp4");  
        FileOutputStream fos=new FileOutputStream("C:\\Users\\李嘉成\\Desktop\\javaStudy\\basic-code\\test\\aaa\\ccc\\paste.mp4");  
        int b;  
        while ((b=fis.read())!=-1){  
            fos.write(b);  
        }  
        fis.close();  
        fos.close();  
        long end = System.currentTimeMillis();  
        System.out.println((end-start)/1000);  
  
    }  
}
```

**read读入数组**

#### 字符集相关的基础知识
**字符集的发展**
- ASCII字符集128个字符，7位就行了，最高位补0
![[Pasted image 20240403111719.png]]
![[Pasted image 20240403111735.png]]
**GBK规则**
![[Pasted image 20240403111944.png]]
- 占两个字节
因为汉字太多，一个字节256个太少，3个字节太浪费
- 最高位的第一位是1
为了区分以一个字节存储的ASCII，这样对于一行数组，如果是0开头，就以一个字节为单位查询ASCII表，如果是1开头，就两个字节为单位查询GBK。 由于GBK兼容ASCII，所以也可以说都是查询GBK表。
**unicode规则**
![[Pasted image 20240403113321.png]]
![[Pasted image 20240403113349.png]]
![[Pasted image 20240403113422.png]]
**出现乱码的原因**
- 读取数据时未读完整个汉字
如果用字节流读取文本文件，将会出现这种情形。但是拷贝不会出现乱码
- 编码和解码的方式不统一
编码解码相同的情形
![[Pasted image 20240403114056.png]]
![[Pasted image 20240403114145.png]]






### 多线程
#### 概念与思想
减少CPU空闲等待的事件，提高CPU的使用效率
比如：
流水线的工人是CPU，流水线上的货物10分钟一次，那么工人除了搬货的事件外，还有空闲等待的时间。 要让工人在空闲等待的时间去做其他的事情，比如大螺丝或者做笔记。
![[Pasted image 20240406114910.png]]
![[Pasted image 20240406145645.png]]
#### 多线程的3种实现方式
##### 方式一：继承Thread
**理论：** 
- 自定义的类MethodOne中，令这个类继承Thread
- 在MethodOne中重写void run(){}方法，将要多线程执行的代码写在这个方法中
- 在测试类创建MethodOne对象mo，通过mo.start()开启线程的执行
评估：
- 优点：编程简单，对象可直接使用Thread类中的方法
- 缺点：由于JAVA是单继承，这将导致不能继承其他类
- 缺点：没有返回值
**类MethodOne定义**
```java
public class MethodOne extends Thread{  
    @Override  
    public void run() {  
        for (int i = 0; i < 100; i++) {  
            System.out.println(getName()+":hello world!");  
        }  
  
    }  
}
```
**Test测试类的调用**
```java
public class Test {  
    public static void main(String[] args) {  
        MethodOne mo1=new MethodOne();  
        MethodOne mo2=new MethodOne();  
        mo1.start();  
        mo2.start();  
    }  
}
```
**输出结果**
```
Thread-0:hello world!
Thread-1:hello world!
Thread-0:hello world!
Thread-0:hello world!
```
##### 方式二：Runnable接口-->可以改造成匿名内部类
本质：在测试类中使用Thread构造方法中的`public Thread(Runnable task)` 
步骤：
- 创建一个类MethodTwo类实现Runnable接口，重写`public void run(){}` 
- 在测试类中创建MethodTwo对象mt ，并创建线程对象`Thread thread=new Thread(mt)`
- thread.start()调用
评估：
- 优点:可扩展性相对更好
- 缺点：没有返回值
##### 方式三：有返回值，实现Callable接口
步骤：
- MethodThree实现Callable接口，重写其中的call方法，call中就是线程返回值
- 在测试类中 调用构造器`public FutureTask(Callable<T>)` 得到对象ft
- 在测试类中，调用构造器`public Thread(Runnable)` 得到对象thread
- thread调用方法start
- ft.get()得到返回值
理论：
- thread调用start方法，所以调用的是thread的run方法，其实就是用的就是FutureTask的。在这个方法中，调用了Call方法，有将返回值赋值给了outcome变量，最后get方法得到返回值。
**MethodTree**
```java
public class MethodThree implements Callable<Integer> {  
    @Override  
    public Integer call() throws Exception {  
        int sum=0;  
        for (int i = 0; i <=100; i++) {  
            sum+=i;  
        }  
        return sum;  
    }  
}
```
**测试类**
```java
public class Test {  
    public static void main(String[] args) throws ExecutionException, InterruptedException {  
       MethodThree mt=new MethodThree();  
       //get方法调用出来的数值是什么，是不是MethodThree中体现的那个值  
        FutureTask<Integer> ft=new FutureTask<>(mt);  
        Thread thread = new Thread(ft);  
        thread.start();  
        System.out.println(ft.get());  //5500
    }  
}
```

outcome的值怎么来的
#### 常用的成员方法
![[Pasted image 20240406161238.png]]

- getName() 
默认名字是`Thread-X` 在构造方法中默认指定的
- currentThread() 
虚拟机默认启动main线程，以前的代码都是运行在这下面的
- setPriority()
与线程调度有关，两种方式抢占式调度（java采用，随机），非抢占式调度（线程轮流）
默认的优先级是5，数值越高抢占到的概率越大，1~10
- setDaemon()
当非守护线程执行结束后，守护线程也会陆续结束。戏称备胎线程，女神没有了，备胎也没有了存在的必要
- yield()
出现cpu的占有权，下次执行再一起竞争
- joint()
设线程t执行在v之上，调用者t.join ,t.start执行完之后，再轮到现v


#### 线程的生命周期
![[Pasted image 20240406164613.png]]
其实
![[Pasted image 20240406220316.png]]
运行状态是自己加上去的
![[Pasted image 20240406220331.png]]
#### 线程的安全问题：同步代码块和同步方法
##### 问题的引入
假设三个窗口要卖100张票，观察原始方式编辑的代码：
###### 阶段一
**输出**
```
Thread-2:卖出了第100张票
Thread-0:卖出了第100张票
Thread-1:卖出了第100张票
```
现象：
- 每个线程独立地售出了100张票，票的数量没有实现共享
原因：
- 每个SellTicket对象相互之间并没有关联，ticket都是从0开始增长的。
解决方式：
- 再ticket前增加修饰词static,让整个类的对象共享ticket变量
**SellTicket** 
```java
public class SellTicket extends Thread{  
   int ticket=0;  
  
    @Override  
    public void run() {  
        while (true){  
            if(ticket<=100){  
                ticket++;  
                System.out.println(getName()+":卖出了第"+ticket+"张票");  
            }else{  
                break;  
            }  
        }  
  
    }  
}
```
**测试类**
```java
public class Test {  
    public static void main(String[] args) throws ExecutionException, InterruptedException {  
        SellTicket s1=new SellTicket();  
        SellTicket s2=new SellTicket();  
        SellTicket s3=new SellTicket();  
        s1.start();  
        s2.start();  
        s3.start();  
    }  
}
```

###### 阶段二：
**输出**
在增加static后，代码运行情况如下：
```
Thread-1:卖出了第95张票
Thread-1:卖出了第99张票
Thread-0:卖出了第97张票
Thread-2:卖出了第98张票
Thread-1:卖出了第101张票
Thread-0:卖出了第101张票
Thread-2:卖出了第100张票
```
现象：
- 既存在一张票多个人卖，又存在超过100张的情况
原因：
- 假设ticket是99，此时A进程执行ticket++,而后B,C 此时ticket为101，而后执行sout
解决办法：
- synchronized包裹代码块，让某个代码执行进入代码块后，其他程序就算抢到cpu执行权，也不能执行块中的内容
###### 阶段三：
问题解决！
输出
```
Thread-0:卖出了第93张票
Thread-0:卖出了第94张票
Thread-0:卖出了第95张票
Thread-0:卖出了第96张票
Thread-0:卖出了第97张票
Thread-0:卖出了第98张票
Thread-0:卖出了第99张票
Thread-0:卖出了第100张票
```

##### 细节
###### synchronized(){}
- ()中的内容必须多个同步线程得是同一个，比较好的参数就是`类名.class` ，一旦不一样，则不能同步，比如在上面代码用this,每个this代表对象不同，最终结果就会和阶段二是一样的
```
Thread-2:卖出了第100张票
Thread-1:卖出了第100张票
```
###### synchronized修饰的方法：
这个方法就是同步的。
![[Pasted image 20240406174044.png]]





#### lock
目的：把三个窗口售票的程序复写一遍



### 网络编程
#### 概念
![[Pasted image 20240407190820.png]]
![[Pasted image 20240407191537.png]]
#### IP
##### 概念
![[Pasted image 20240407191932.png]]
![[Pasted image 20240407192634.png]]
**如何解决ip不够的情况：**
![[Pasted image 20240407192711.png]]
同一个局域网的设备用192.168开头的私有地址，这些设备共享同一个Ip地址。
##### 在java中获取IP对象，InetAddress类
有Inet4Address 和Inet6Address两个子类
![[Pasted image 20240407193826.png]]
#### 端口号
![[Pasted image 20240407194248.png]]
#### 协议
##### 概念
![[Pasted image 20240407194743.png]]
##### UDP
###### 理论
![[Pasted image 20240407194754.png]]
**应用场景**
在线视频、语音通话、网络会议
**利用udp发送数据**
- 绑定发送的端口 DatagramSocket对象
确定发送地址，有65536个发送地址，对于接受方来讲，发送方地址是无所谓的。
-  将要发送 的数据打包成一个数据包， DatagramPacket
要封装ip和端口号，相当于接收方的接受地址。
要封装数据，没有数据就没有意义了。
- 发送
给句2中的地址，将数据发过去
- 关闭资源
**利用udp接受数据**
- 指定接受的地址DatagramSocket对象
这个地址要和发送端发送数据时绑定的Socket匹配
- 要准备一个箱子接受数据，这个箱子里要装一个BUFFER,DatagramPacket
- 用箱子接受数据
阻塞的
- 对箱子内的东西进行解析
- 关闭
**三种通信方式**
###### 代码：单播，组播，广播
**单播**
发送端
```java
public class SendMessageDemo {  
    public static void main(String[] args) throws IOException {  
        //绑定本机的发送该数据包的端口，未指定，随机确定端口号  
        DatagramSocket ds=new DatagramSocket();  
          
        //封装要发送的数据包，包括接收端的ip port 和发送的数据message  
        InetAddress ia=InetAddress.getByName("127.0.0.1");  
        int port=15503;   
        String message="你好，我在用udp跟你发送消息！";  
        byte[] bytes = message.getBytes();  
        DatagramPacket dp=new DatagramPacket(bytes,bytes.length,ia,15503);  
          
        //发送数据  
        ds.send(dp);  
        //关闭资源，由于udp是无连接不可靠的，发完数据后立马会关闭  
        ds.close();  
    }  
}
```
接收端
```java
  
public class ReceiveMessageDemo {  
    public static void main(String[] args) throws IOException {  
        //指定接收地址，ip就是本机，唯一要确定的是端口号，所以一定得加上  
        DatagramSocket ds=new DatagramSocket(15503);  
  
        //准备接收数据的篮子bytes  
        byte[] bytes=new byte[1024];  
        DatagramPacket dp=new DatagramPacket(bytes,bytes.length);  
  
        //接收数据  
        ds.receive(dp);  
  
        //解析数据包，包括数据，发送方的inetAdress，端口号  
        byte[] receiveMessageByte = dp.getData();  
        String receiveMessage=new String(receiveMessageByte);  
        InetAddress address = dp.getAddress();  
        int port = dp.getPort();  
        //做适当的打印输出  
  
        System.out.println("信息来源于"+receiveMessage+":"+port+"，数据是"+receiveMessage);  
        //关闭流  
        ds.close();  
  
    }  
}
```
**组播**
发送端相比于单播的区别：
- 不再使用DatagramSocket，而是使用MulticastSocket
- 指定接收端的ip时，使用组播的ip，范围是
![[Pasted image 20240407214855.png]]
接收端相比于单播的区别：
- 不再使用DatagramSocket,而是使用MulticastSocket用于指定接收地址，port仍然不变，但是得让接收对象加入到组播中， `ms.joinGroup(ip);  `
发送端
```java
  
public class SendMessageDemo {  
    public static void main(String[] args) throws IOException {  
        //发送数据端口号  
        MulticastSocket ms=new MulticastSocket();  
  
        //发送的数据  
            //ip与端口号  
        InetAddress ip=InetAddress.getByName("224.0.0.1");  
        int port=10025;  
            //Scanner获取要发送的数据，并转成bytes数组  
        Scanner sc=new Scanner(System.in);  
        System.out.println("输入要发送的数据：");  
        String sendMessage = sc.nextLine();  
        byte[] bytes = sendMessage.getBytes();  
            //将上面的数据封装在datagrampacket中  
        DatagramPacket dp=new DatagramPacket(bytes,bytes.length,ip,port);  
  
        //发送  
        ms.send(dp);  
        //关闭资源  
        ms.close();  
    }  
}
```
接收端
```java
  
public class ReceiveMessageDemo {  
    public static void main(String[] args) throws IOException {  
        //指定接收地点-->组播地址+端口号  
        MulticastSocket ms=new MulticastSocket(10025);  
        InetAddress ip=InetAddress.getByName("224.0.0.2");  
        ms.joinGroup(ip);  
  
        //制作接收消息的篮子  
        byte[] receiveMessageByte=new byte[1024];  
        DatagramPacket dp=new DatagramPacket(receiveMessageByte,receiveMessageByte.length);  
  
        //接收数据  
        ms.receive(dp);  
  
        //解析数据包  
        InetAddress address = dp.getAddress();  
        int port = dp.getPort();  
        String receiveMessage = new String(dp.getData());  
        System.out.println("数据来自于"+address+":"+port+",接收到的数据为"+receiveMessage);  
  
        //关闭资源  
        ms.close();  
    }  
}
```
**广播**
测试方法：
多开接收端，，让多个接收端处于
代码与单播的区别：
- 发送接收地址的DatagramSocket改成MulticastSocket
- DatagramPocket的ip改成255.255.255.255，其他与单播没有任何区别


##### TCP
###### 理论
![[Pasted image 20240407194841.png]]
**对三次握手的理解**
网络上发送了一个消息后，并不能确定对方是否收到，所以对方的发送消息回来才能确定：
对于客户端，发送一个，接收一次，就确定知道服务端知道了，但是服务端不知道客户端知道了，所以客户端还要再发送一次。
- 客户端向服务端发送连接请求-->客户端并不知道服务端收到了这个请求
- 服务端向客户端发送同意连接请求-->客户端知道了服务端收到了请求，服务端不知道客户端收到了请求
- 客户端向服务端发送收到同意连接请求-->服务端知道了客户端收到了请求
![[Pasted image 20240407223931.png]]
**对4次挥手的理解**
- 客户端发送断开连接请求 -->客户端不知道服务端收到了
- 服务端发送收到了断开连接请求-->客户端知道了服务端收到了断开连接请求
- 等到服务端把io读取完成
- 服务端发送断开连接请求-->服务端不知道客户端是否收到
- 客户端回送断开连接请求-->服务端知道了
![[Pasted image 20240407223719.png]]


**应用场景**
软件下载、文字聊天、发送邮件
### 反射
##### 作用，总结，意义
![[Pasted image 20240404223504.png]]
##### 获取Class(Class是一个类)对象的三种方法
![[Pasted image 20240404212725.png]]
方法一最常用
方法二常用于传递参数
![[Pasted image 20240404212848.png]]

##### 通过反射获得构造方法
- 调用Class中的方法，返回值为Constructor类型的对象
![[Pasted image 20240404215139.png]]
说明：不带Declared的方法，返回所有被public修饰，包含父类的属性和方法
带Declared修饰的不包含父类，但是本类中定义任意修饰符定义的都会被访问
- 利用获得的构造方法对象：创建对象
![[Pasted image 20240404215237.png]]
说明：setAccessible使用之后才能调用private修饰的构造方法和成员方法
 - 利用获得的构造方法对象：获得权限修饰符，参数表
 ![[Pasted image 20240404215325.png]]
 注意：获得的权限修饰符以整数的形式返回的，具体哪儿个数字对应啥，reflect.Modifier中可查

##### 通过反射获得成员变量
- 通过调用Class中的方法来获得Filed对象
![[Pasted image 20240404220542.png]]
- 对获得的FIled对象，获得其修饰符，值
- 对获得的Filed对象，对指定的对象对于这个属性进行赋值
![[Pasted image 20240404220722.png]]
##### 通过反射获得成员方法

![[Pasted image 20240404222320.png]]
作用与上面类似
### 动态代理
**思想**
![[Pasted image 20240404224321.png]]
![[Pasted image 20240404224346.png]]
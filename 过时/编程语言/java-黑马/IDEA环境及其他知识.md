#### 快捷键
- alt+insert -->选择constructor/getter/setter -->选择对应的属性 
快速生成对应的构造方法和get和set方法
或者使用ptg插件，右键点击插件，快速生成javabean
- ctrl+alt+v 
自动根据数值生成左边，并且加上分号
如：18 --> int [v] =18;
- ctrl+b   <-->ctrl+鼠标左键
对于选中的方法，按ctrl+b,能够跳转到对应的源码区域
- ctrl+alt+t
对于选中的内容，按 ctrl+alt+t能够快速的追加if for等条件分支语句
- ctrl+n
搜索的快捷键
- ctrl+/
对选中的内容进行注释
- ctrl+p (parameters)
提示函数的参数列表中的参数顺序与类型
- 鼠标放在红色波浪线上
弹出错误原因的提示
- alt+回车
弹出建议的修改意见
- end
跳转到本行的最后
- ctrl+end
整篇的最后一行
- ctrl+alt+m  （m<->method）
将选中的代码抽取出来，形成一个函数
- alt+shift+上下箭头
快速地交换行与行
**选择** 
- ctrl+a 
全选
- ctrl+鼠标左键
同时选择指定的多个
- 左键+shift+左键
选择起始到结束
- alt+鼠标左键 或者 按住滚轮(按下去)，选择
竖向选择
**---------------------------------**


#### 简写
- psvm
```java
public static void main(String[] args){

}
```
- sout
`System.out.println();`
- 变量名/值.sout
`System.out.println(变量名/值)`
**遍历** 
- 数组名.fori
```java
//还有其他两种
for(int i;i<数组名.length;i++){

}
```
- 单列集合和数组名.for
```
for(){

}
```
* 字符串.length().fori
```java
for (int i = 0; i < s.length(); i++) {  
      
}
```
#### 操作
- 查看接口方法的实现
选中方法->右键->go to->implements->弹出的所有实现类中，寻找自己需要的
- 重写object中的equals方法，改地址判断为属性判断
alt+insert->equals() and hashcode() ->傻瓜式地下一步就ok了
- 复制全类名
找到类所在的java文件->选中类名->copy/paste special->copy reference
当粘贴在”“ 或者注释中时候，全类名，当粘贴在空白处时，只是类名
`CountUseTImes` 与`edu.hebut.filetest.CountUseTImes`

#### 颜色
- 灰色的关键字 
不写也不会错

**打开CMD窗口：** 
win+R cmd 回车

#### 操作
- 查看字节码文件
在idea中编写代码的界面内，右键->open in->explorer 
切换到项目文件夹下面，选择out文件夹
对应于包的情况，进行查询对应的类的字节码

**常见名称：**
E: 盘符切换
dir 查看当前路径下的内容
cd .. 回退上一级目录
cd \ 回到盘符的根目录
cd 目录  进入单级目录
cd 目录1\目录2\… 进入多级目录
cls 清屏
exit 退出CMD 

**环境变量：**
先检测当前目录是否有该执行文件，如果没有则在环境变量中查找

**LTS** 长期支持版本

### IDEA


### 
**IDEA的项目结构介绍** 
在模块的src下创建包
![[Pasted image 20240313214621.png]]
### 包： 
**包名**常用公司域名的反写，对于我来讲就写 edu.hebut.stu 
包是一个文件夹，edu.hebut.stu 是多级包


#### settings
1、主题
2、字体consolas
3、自动导入包
4、提示忽略大小写

#### 操作
1、修改类名 用refactor
2、关闭项目
3、split right //两个文件同时呈现画面中





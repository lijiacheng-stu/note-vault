### 基本的方法
![[Pasted image 20240412101153.png]]
### 目标:实现页面之间的跳转操作
步骤：
- 创建类文件和与之对应的xml文件
- 对xml文件进行编辑
LinearLayout
butten
textview
控件编辑的思考角度：
**定义**
命名id：规范元素的类型_功能
**布局**
本身的大小：layout_widthlayout_width layout_height
按键所处所处于页面的位置：gravity ?
**内容**
text
- 在类文件中实现控件的逻辑功能，实现形式的通过绑定监听：
	- 首先是通过id找到控件：findViewByid(R.id.控件名称)
	- 然后设置对其设置点击监听事件：setOnClickListener()
	- 最后实现onClick()函数：
- 在manifest文件中进行 注册

### Activity生命周期
![[Pasted image 20240412102238.png]]
主要掌握的路径：
- 打开新页面：参考系是新页面
onCreate-->onStart-->onResume
- 关闭旧页面：参考系是旧页面
onPause-->onStop-->onDestroy
- 在旧页面上打开新页面：参考系为旧页面
onPause-->onStop
- 关系新页面，重新显示旧页面：参考系为旧页面
onRestart-->onStart-->onResume
![[Pasted image 20240412102152.png]]




	

### Activity启动模式
#### 在java中进行设置
通过设置intent意图来实现，跳转到新Activity时采用的跳转模式：重要的Intent类方法：
`Intent setFlags(int flags){}`  
![[Pasted image 20240412105039.png]]
常见的标志以及其含义：
![[Pasted image 20240412105542.png]]
#### 在配置文件中进行设置
设置launchMode属性
![[Pasted image 20240412105633.png]]
![[Pasted image 20240412105737.png]]

### 显式Intent和隐式Intent
#### 显式Intent
![[Pasted image 20240412111656.png]]


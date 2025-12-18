知识凝练：
1.Unity uses a left-handed coordinate system

2.Placing one near each corner should be fine (I suggest raising them to the tops of the walls), plus one placed high above the scene (for example, a Y position of 18) to give variety to the light in the room.

3.transforms包含三个：Translate, Rotate, and Scale

4.Public variables are exposed in the Inspector so that you can adjust the component’s values after adding a component to a game object. This is referred to as serializing the value, because Unity saves the modified state of the variable.


5.航空学中描述旋转的方式与此类似，因此从事3D图形开发的程序员常常借用一组航空术语：**俯仰（pitch）**、**偏航（yaw）**和**翻滚（roll）**。如图2.13所示：
- **俯仰（pitch）**：绕X轴旋转（类似飞机抬升或俯冲）
- **偏航（yaw）**：绕Y轴旋转（类似飞机左右转向）
- **翻滚（roll）**：绕Z轴旋转（类似飞机侧身翻滚）
![[Pasted image 20250517114640.png]]


6.使运动速率与帧率无关
有关（ frame-rate dependent）的原因：
- 对于update()方法是每一帧都执行一次。
```
transform.translate(5,0,0)
```
每一帧移动5个单位，则30帧率下就是150单位，60帧率下就是300单位
- 如何做到无关
首先定义一个速度，单位是（移动单位/s）`float speed = 9.0f`
然后确定每一帧的移动距离，距离=速度/帧数。 1/帧数 = Time.deltaTime

7 版本控制，其中gitignore的文件网址： `https://github.com/github/gitignore/blob/main/Unity.gitignore`

总结:
1.布置场景
- Cube：Inner Wall，OuterWall
- Light：point light，directional light
- Capsual，Camera：Player

2.获取输入
Input.GetAxis()
- Axis是通道的意思，不同的通道对应不同的输入。
- 返回值再-1,1之间
- 鼠标：`"Mouse X","Mouse Y"`
- 键盘：`"Horizontal","Vertical"`

3.transform：rotation,translate
3.1 通识
- 坐标：全局坐标系（global，Space.World），本地坐标系统
	- 本地坐标系：
		- 在transform.Rotate()等中，默认是本地坐标系。相对的是本Object的坐标系
		- 在层级结构(Building/Outer Wall，Floor)中，子Object的transform属性相对的是父Object
	- 全局坐标系
		- 在transform.Rotate()等中，第四个参数Space.World，可切换全局。
		- characterController.Move(movement)接收movement是Vector3类型，相对的是全局坐标系的向量
		- transform.transformDireaction(movement)将movement看成本地坐标系下得出得向量，转成全局坐标系。参考系只是对相同事物不同角度的观察结果，本质是不变的。
- transform的两种策略：
	- 给移动的向量：
	```
	characterController.Move()
	transform.rotate()
	```
	- 给移动的位置：
	```
	transform.localEulerAngles = new Vector3()
	```
- 数值处理的方法
```
Mathf.clamp(var,min,max); //将数值限定在某个范围
Vertor3.clampMagnitude(movement,speed); //限定向量的模长
```
3.2 鼠标让视角移动
- 命名规范
```
RotationAxes(MouseX,MouseY,MouseXandY) //用于旋转的通道
sensitivityHor //水平灵敏度，单位时间旋转的欧拉角
sensitivityVer //垂直灵敏度

rotationHor //当前水平旋转角度y
rotationVer //垂直旋转最终角度x

deltaHor //每帧水平旋转角度
deltaVer //每帧垂直旋转角度

```
- 算法:
接收鼠标运动返回值Input.GetAxis("Mouse X")，
确定deltaHor 每帧旋转角度`Input.GetAxis("Mouse X") * sensitivityHor * Time.timeDelta`
（可选）确定rotationHor最终旋转角度  `rotationHor += deltaHor `
指定下一帧的位置`transform.localEulerAngles = new Vector3()`

3.3 键盘让人物移动
确定移动的向量相对于Player而言：
- 确定每个方向移动的分量
- 对长度进行限制
计算移动后的位置：
- 移动分量（也得相对于global）
刷新之后的位置
- 获得characterController
- 调用Move方法






总结：
基础知识：

- 坐标系有两个，一个是local，一个是global。对于local以当前object的position为原点，rotation为x，y，z建立坐标系；global则是全局的，对于所有object都是统一的。
```
//默认是local，可以用第四个参数Space.World切换成global
transform.Translate();
transform.Rotate();
transform.scale();

//当前component，全局移动
characterController.Move(vecter3);

//当前component，相对于全局的角度
transform.LocalEulerAngles = new vector3()

//将local的向量转成global下的向量；向量本质上完全一样，只是表述不一样
//该方法意义很大，用于将local的变化，弄成global的变化
transform.TransformDirection(vecter)
```
- 根据鼠标和键盘记录数值,配合Speed，来确定各个分量的Delta，最后确定运动向量，必要的时候，转化成
	- Mouse X：范围-1~1，根据鼠标X轴运动速度决定大小，左右决定正负
	- Mouse Y：范围-1~1，根据Y轴
	- Horizontal： A=-1 D=1，具体可以看Edit>project setting>Input Manager
	- Vertical: S=-1 W=1
```
Input.GetAxis("");
```
- 两个Clamp
```
Vector3.ClampMagnitude(Vector3,speed);
Mathf.Clamp(va,min,max)
```


场景布置：
- 场所：通过GameObject中的Cube布置了Floor和Outer Wall，把这些放在Building这个层级，成为一个整体
- 灯光：通过GameObject中的point light和directional light布置了灯光
- 人：通过GameObject中的sphere设置了Player，通过GameObject中的camera设置了Player的视野，并把camera放在Player下面


如何让小人能够移动呢？


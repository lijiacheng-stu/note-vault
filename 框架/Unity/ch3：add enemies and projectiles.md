1. 对raycasting的理解：
- raycasing = cast a ray into the scene
- ray = a ray is an imaginary or invisible line in the scene that starts at a point of origin and extends out in a specific direction.
- 涉及的操作是：怎样射出ray？和ray相交的物体会怎么样？

2.  发射光线的方法
2.1 核心要点：定义光线`起点终点 或 [光线起点 + 光线方向]`  + 投射 
2.2 定义光线
- Camera定义光线：
```
 Ray Camera.ScreenPointToRay(Vector3 point);//起点就是camera，终点是point，像素
```
- 由任意物体发射光线：
```
Ray ray = new Ray(transform.position, transform.forward); //光线起点 + 光线方向， transform.forward是local坐标系的z轴方向
```
2.3 投射
- 参数：用于投射的光线，用于获取相交点信息的hit
```
 public static bool Physics.Raycast(Ray ray, out RaycastHit hitInfo);
 //raycast = 发射光线 + 相交点
```
- hit的用法：
	- 通过raycasthit的point属性，可以用于对相交点进行放置东西。（Player放置了球）
	- 通过raycasthit的distance属性，可以用于判断当前物体距离对象的距离。（监测与墙体的距离，小于则绕y轴旋转）
	- 通过raycasthit的transform属性，就是碰撞对象的transform组件，继而知道该对象`GameObject gameObject = hit.transform.gameObject`
		- 身份识别: 通过判断该对象是否具有标识身份的组件来判断身份。如`PlayerCharacter playerCharacter = hitObject.getComponent<PlayerCharacter>()` ，通过该身份向外提供的用于操作该对象的方法进行操作。`playerCharacter.hurt(1)`
		- 控制对象：通过控制组成Object的components中的属性来控制对象

3. 回溯component挂载的Object：可以用任何组件回溯到其其所属的GameObject，如`transform.gameObject`
- tips：PaycastHit有属性组件Transform，配合3中的性能就能找到命中的gameObject
`GameObject hitObject = hit.tranform.gameObject`
- 一种思路：hit -> hitObject -> a component of hitObject -> a method of the component


4.  coroutine协程的理解（与普通函数的区别的角度）：
- 作用：
普通函数：不能停滞。确保每一帧的时间能执行完一次update()。且调用普通函数，函数执行完，才能回到主函数。
IEnumerator函数： 可以停滞(`yield return new WaitForSeconds(1);`),且一旦停滞回到主函数，剩下的代码系统自动执行。每一次调用都不想干（也就是说可能并行有好几个IEumerator函数）
- 调用
普通函数：主函数用`函数名()`
IEnumerator函数：`startCoroutine(函数名())`


5.  `[SerializeField] vs public vs private` 
- private：不能被其他script修改，不能被展示在Inspector
- `[SerializeField]` ：不能被其他script修改，但是能在Inspector中展示
- public ：都能
- 黑话：变量被Unity序列化了 = 变量能被Inspector中看到 

6.  OnTriggerEnter的触发条件：
当判定为触碰时，执行该方法。怎样判定触碰呢？
- 碰撞双方都有collider，其中Character Controller属于特殊地collider
- 至少一方有Physics->rigid body
- 至少一方的collider中勾选Is Trigger

7. 对象的理解：
- 一个对象是一个组件容器，除此之外什么都没有。
- script是组件的前提是继承MonoBehaviour。
	- script能通过getComponent获得同一级别的组件。通过对获取的组件进行属性设置，来调整对象。如：获取组件transform，调整position，rotation，scale相关的东西，控制对象。
	- 对象至少有transform组件。所以script可以直接访问transform而没有安全风险，不需要`getComponent<Transfrom>()` 操作
- 任何组件都有gameObject属性用于获得其父对象。

8. 对prefab的理解（个人）：
 - 本质：与OOP中的“类”相似，可用于创建具体的实例。注：类型也是GameObject。
- 创建prefab：将hierarchy中的对象拖动到project窗口，就创建了该实例的prefab
- 作用：生成对象

9. 生成一个对象的方法：
- 生成对象
	- 通过prefab生成：`enemy = Instantiate(enemyPrefab) as GameObject;`
	- 通过内置的类型生成：` GameObject sphere = GameObject.CreatePrimitive(PrimitiveType.Sphere);`
- transform组件，利用该组件的属性或者方法对组件的为位置，旋转，运动。




总结
1.本节的的思路：
- 前提：已经完成对场景的布置，完成Player觉得的移动和mouselook视野的功能
- 过程：
	- 点击按钮的时候能发射Ray，让被射到光线的地方出现弹坑，让中间出现瞄准的中间镜头
	- 创建Enemy，让Enemy移动，遇到障碍物后，随机旋转角度避障，被子弹射到后会躺下，数秒后消失
	- 消失后，能够重新产生新的Enemy
	- Enemy识别到Player后能产生火球
	- 火球能向前运动，碰撞到物体后消失，碰撞到人后，人掉一滴血



2.体会：
- 一定要有对象的思维。
	- 体现一：身份组件。EnemyCharacter，PlayerCharacter，FireballCharacter用于代表Enemy，Player身份，封装了拥有该身份的一切操作和被操作的方法。
	- 体现二：只管创建，创建后怎么样不管。创建火球后（火球本体和对属性初始化），火球怎么样由火球自己决定(FireballCharacter)。
	(所以对子弹也是可以优化的，这样就不需要协程来控制子弹的消失。)

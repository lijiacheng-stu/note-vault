![[Pasted image 20261028112801.png]]
## 1. 核心问题：C和V之间是怎样互动的？
- 选择那儿一个？
- 怎么传递数据给对方？
- 怎么解析对方传递过来的数据？
### 1.1 从C的视角：
- return "design"，选择了/java/resources/templates下面的view，并将model传递给view
- 通过model对象。
	- 增加model对象的属性
	- 通过引用model，手动增加model属性
	- @RequestParam
- 通过构建一个对象，例如ResigistraionForm，然后让参数填充那个对象
- 注意：C也可以用return "redirect:/login"来访问其他的Controller

### 1.2从V的视角：
- 视图通常通过用户操作发起新的 HTTP 请求，而不是直接调用 Java 控制器方法

## 2. 常见的机制
- 浏览器访问 `http://localhost:8080/register` 并发送 GET 请求
- RegistrationController 接受GET请求，并返回registration.html给客户端浏览器
- 用户填写并提交表单，向`http://localhost:8080/register` 并发送POST 请求
- RegistrationController 接受POST请求，将POST中的内容存储为一个对象，以存储注册的用户，并返回login.html
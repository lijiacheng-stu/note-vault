CSRF = cross-site request forgery 跨站请求伪造
```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Cookie: session=yvthwsztyeQkAPzeQ5gHgTvlyxHfsAfE

email=wiener@normal-user.com
```
- 当用户user登陆b.com后，用户的浏览器中会保存一个关联这个网站的cookie，这个cookie中有一个字段就是sessionid。服务器会把用户登陆信息存储在session中，通过sessionid进行索引。cookie中的sessionid就能够验证请求这的身份。
- b.com发送对b.com的post请求是这样，a.com对b.com的post请求也会读取存储在浏览器中b.com的cookie，这样就不知道是谁发起的了。有一些敏感的操作，是必须b.com发送才行的，怎么解决呢？
	- 方法一：SameSite cookies。a.com对b.com的post请求，浏览器不携带b.com的cookie了。
	- 方法二：**CSRF tokens**
		- 服务器端有**CSRF tokens** 字段，并且会在渲染html前注入到request attribute中，让html中的表单进行引用成一个隐藏属性。这样post后，携带这个属性，就可以用于检验了。
	- 方法二：**Referer-based validation**：浏览器根据策略添加`Referer: https://a.com/page`,用以表明是谁发起的POST请求，服务器端验证起内容。但是可能各种各样的原因缺失。
- 这是一个修改用户email的Http Request

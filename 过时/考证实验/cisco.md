## 等价关系
- interface 和int等价
## 知识
### 路由器配置
#### 1.查看命令
##### 查看路由表
- 特权模式下，show ip route
#### 2.IP地址和子网掩码的配置
##### 命令行
- 入口：CLI (command line)
![[Pasted image 20240710161102.png]]
- 用户模式-en-特权模式- configure-全局配置模式-interface g0/0-接口配置模式-exit-退回到前一级模式
- 显示端口 option->preferrence
![[Pasted image 20240710152646.png]]
- 配置完接口后，得使用no shutdown命令，打开端口
##### gui界面
- 入口
![[Pasted image 20240710161307.png]]

#### 3.路由协议的配置
##### 静态路由的配置
在全局配置模式下：
1.   
    Router(config)ip route 192.168.2.0 255.255.255.0 1.1.1.2
### PC主机的配置
- 图形化界面配置

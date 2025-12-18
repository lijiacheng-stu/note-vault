## 0.常用指令
- linux
```
ping ip/domain //查看连通性，配合arp
arp -a //查看本网络中的主机
ip a //查看本机的ip和mac，分别包括ipv4和ipv5下的，ip地址广播地址，mac地址

```
- windows
```
ping ip/domain //查看连通性，配合arp
arp -a //查看本网络中的主机
ipconfig /all //查看本机的ip和mac
```
## 1.NAT模式
1. 若VMware中开启多个虚拟机，网络模式是Nat network的形式 还是 nat的形式
![[Pasted image 20251108163502.png]]
2. WSL的
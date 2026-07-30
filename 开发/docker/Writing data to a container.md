- 终端模拟器，如何连接其他的master？
- tty，终端模拟器，session，进程组之间的关系？
- 如何理解docker attach container_name？
- docker run -it的意义？

### 问题2
当打开一个终端模拟器的时候，除了打开终端模拟器进程外，还会打开一个shell进程，申请一个pty(伪终端)。pty有两段slave端和master端，slave端连接shell进程，master端连接终端模拟器进程。slave端在shell进程看来和一个正常的物理终端没有任何区别。终端模拟器从master端输入的东西，会从slave输出被shell读；shell写入slave的东西，会从master输出被终端模拟器读。在这两个端口中间存在line discipline，用于逐行输入输出，而且可以修改一些内容，把特殊的字节转化正signal发送出去等。使line discipline失效的模式就是raw mode。
一个session会分配一个tty，一个session中有多个进程组。所有的进程组都连在tty上，但是从tty读数据的资格给其中一个进程组，被分配到tty的进程组叫做foreground process group，没被分配到的叫做background process group。`fg 1`用于把background process group成为foreground process group；还有`bg`。jobs可以看到当前shell进程所关联的所有background process group。


### 问题3
存在一个pty，它的slave端连接container中的shell进程上，master端口被Linux VM里的一个进程连接着，并且这个进程可以以某种通信协议与宿主机中的进程通信。
宿主机，在docker attach container_name后，启动一个进程，它专门与连接master端口的进程进行通信。这个进程同时也连在宿主机的另一个pty的slave口与连接对应的master口的终端模拟器以raw mode通信。
ssh也是这样的原理。





docker中，实现docker attach的原理是：
- 在容器侧，shell程序启动，并且连在了pty的slave端；又一个程序连在master侧，这个程序有一个网络端口，将从master侧读到的发送出去，将从网口侧读到的写到master侧；
- 在local macine侧，有一个进程，它通过网络与在容器侧的master侧的进程进行通信。这个进程本身连在了一个pty的slave侧，而pty的master侧连在了terminal emulator。这个模式是raw模式。

## 问题2


如何上面的理论是正确的，那么正在运行的background process group的输出，其输出可以直接通过tty输出到终端模拟器上，但是不接受`ctrl + C`和`ctrl + Z` 。
lijiacheng@lijiachengdeMac-mini-5 unix % cat pcircle.c 


## 问题3

可以看到config.cm= "/bin/bash"，也就是启动基于这个image的container会执行此命令
lijiacheng@lijiachengdeMac-mini-5 unix % docker inspect ubuntu:latest

"Config": {

            "Env": [

                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

            ],

            "Cmd": [

                "/bin/bash"

            ],

            "Labels": {

                "org.opencontainers.image.ref.name": "ubuntu",

                "org.opencontainers.image.version": "24.04"

            }

        },
正如刚才所料：
lijiacheng@lijiachengdeMac-mini-5 unix % docker ps -a

CONTAINER ID   IMAGE                              COMMAND                   CREATED        STATUS                      PORTS                    NAMES

230b03e950e9   ubuntu:latest                      "/bin/bash"               17 hours ago   Exited (0) 16 hours ago                              myubuntu4

这样实现了启动：
lijiacheng@lijiachengdeMac-mini-5 unix % docker start myubuntu4

myubuntu4

lijiacheng@lijiachengdeMac-mini-5 unix % docker ps

CONTAINER ID   IMAGE           COMMAND       CREATED        STATUS         PORTS     NAMES

230b03e950e9   ubuntu:latest   "/bin/bash"   17 hours ago   Up 5 seconds             myubuntu4


现在我们这个终端连接的tty,是这个东西
lijiacheng@lijiachengdeMac-mini-5 unix % tty

/dev/ttys001


让这个模拟器连接其他的tty：

lijiacheng@lijiachengdeMac-mini-5 unix % docker attach myubuntu4

root@230b03e950e9:/# tty

/dev/pts/0


上面的推理正确吗？
如果正确，我现在对myubuntu4中bash给退了，那么这个终端应该处于游离状态，但是事实回退回了原tty：
root@230b03e950e9:/# exit

exit

lijiacheng@lijiachengdeMac-mini-5 unix %




- 终端模拟器，如何连接其他的master？
- tty，终端模拟器，session，进程组之间的关系？
- 如何理解docker attach container_name？

## 问题2

一个session会分配一个tty，一个session中有多个进程组。所有的进程组都连在tty上，但是从tty读数据的资格给其中一个进程组，被分配到tty的进程组叫做foreground process group，没被分配到的叫做background process group。
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




问题：
- ssh登陆服务器，会创建远端登陆Shell，在shell中执行训练命令，此时命令执行进程是shell进程的子进程。当出现断网后，ssh断开，shell进程关闭，训练也将中断。因此，问题出现在， Shell进程会受到网络影响，继而波动到依赖shell进程的session。所以，实现shell 和session的分离就好了。

基本的操作需求：
- 
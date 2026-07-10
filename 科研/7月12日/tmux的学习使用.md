问题：
- ssh登陆服务器，会创建远端登陆Shell，在shell中执行训练命令，此时命令执行进程是shell进程的子进程。当出现断网后，ssh断开，shell进程关闭，训练也将中断。因此，问题出现在， Shell进程会受到网络影响，继而波动到依赖shell进程的session。所以，实现shell 和session的分离就好了。

理论基础：
- 通常，打开一个终端窗口的同时会启动一个shell进程，这个进程属于一个以这个shell进程为session leader的session，shell执行新的命令产生的进程会属于此session，且以shell进程为父进程。关闭窗口，会关闭这个shell进程，其子孙进程都会关闭。（即，打开一个窗口，开启一个session， 关闭窗口，关闭这个session）
- tmux通过tmux client和tmux server实现，session和窗口的解耦,  即窗口的关闭，不会使得session关闭。打开一个终端，即打开了tmux client，通过 `tmux` 或`tmux new -s <session-name>` 创建新的session，启动tmux server，并且在server下创建新的session，并且让此client与这个session进行了attach， 在tmux client显示session的内容。当关闭窗口后，关闭tmux client，但是并没有关闭tmux server。
- 涉及tmux client和server两端四类操作（增删改查）：
	- 通用的操作：
		- `tmux ls`
		- `tmux kill-session -t 0`
		- `tmux rename-session -t 0 <new-name>`
	- tmux server内，session_A对session_B的操作:
		- `tmux switch -t 0` 切换session
	- tmux server内，session对自己的操作:
		- `tmux detach` ,切断tmux client对当前tmux session的连接，回归到tmux client自己的窗口，是tmux attach的逆操作
	- tmux server外的session，即 tmux client，对tmux server内的session的操作
		- `tmux` 或`tmux new -s <session-name>` 创建新的session
		- `tmux attach -t 0`


基本的操作需求：
1. 安装tmux，尤其是在linux系统
2. 在tmux server创建一个新的session
3. 在tmux client连接tmux server中的一个session
4. 在tmux server中的session关闭自身
5. 在其他session中关闭tmux server中的session




具体的流程：
#### 对需求1：
- `uname -a`  查看系统的类型
- `sudo apt-get install tmux` 针对linux系统

#### 对需求2：
- `tmux` 或 `tmux new -s <session-name>`

#### 对需求3：
- `tmux ls` 
- `tmux attach -t 0`

### 对需求4:
- `exit`

### 对需求5
- `tmux kill-session -t 0`

在local host的terminal使用`docker exec`或`docker run`，令container执行命令时，会在local host开启新的进程，用于至少接受这个进程的输出流。 可以通过-d来让这个新进程成为守护进程(其实是直接kill)，避免终端一直等。可以通过ctrl+c关闭这个local host进程也行，但是会脱离监管。

docker run --rm -d alpine sleep 20




docker run 
- --name 给容器命名
- -it 是否给主进程配pty，是否让terminal emulator的输入流能与主进程互动
- --restart  配置容器的重启策略
- --rm 配置容器关闭后是否删除
- 命令，配置启动主进程的命令，可以覆盖CMD，但是无法覆盖entrypoint

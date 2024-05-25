在Docker中，可以使用交互式模式来与容器进行交互，这样可以像在本地计算机上一样在容器内执行命令。

创建运行一个容器并进入容器 shell 交互模式
**docker run -it ubuntu**
进入一个正在运行的容器 shell 交互模式
**docker container exec -it webhost sh**

在命令中，-i 表示交互式，允许您与容器进行交互，-t 表示分配一个伪终端（pseudo-TTY），这样您就可以在容器内部执行命令。

```
C:\Users\weick>docker container ls -a
CONTAINER ID   IMAGE     COMMAND                   CREATED          STATUS          PORTS                NAMES
6fc95d84c1be   nginx     "/docker-entrypoint.…"   13 minutes ago   Up 13 minutes   0.0.0.0:80->80/tcp   webhost

// 创建运行一个容器并进入容器 shell 交互模式
C:\Users\weick>docker run -it ubuntu
root@e37510525792:/# ls
bin  boot  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
// 退出容器 shell 交互模式
root@e37510525792:/# exit
exit

C:\Users\weick>docker container ls -a
CONTAINER ID   IMAGE     COMMAND                   CREATED          STATUS                     PORTS                NAMES
e37510525792   ubuntu    "/bin/bash"               20 seconds ago   Exited (0) 4 seconds ago                        hopeful_rhodes
6fc95d84c1be   nginx     "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes              0.0.0.0:80->80/tcp   webhost

// 进入一个正在运行的容器 shell 交互模式
C:\Users\weick>docker container exec -it webhost sh
# ls
bin   dev                  docker-entrypoint.sh  home  lib64  mnt  proc  run   srv  tmp  var
boot  docker-entrypoint.d  etc                   lib   media  opt  root  sbin  sys  usr
# exit

C:\Users\weick>docker container ls -a
CONTAINER ID   IMAGE     COMMAND                   CREATED          STATUS                      PORTS                NAMES
e37510525792   ubuntu    "/bin/bash"               46 seconds ago   Exited (0) 29 seconds ago                        hopeful_rhodes
6fc95d84c1be   nginx     "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes               0.0.0.0:80->80/tcp   webhost

C:\Users\weick>

```
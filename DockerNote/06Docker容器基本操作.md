## 容器命令
官方文档：https://docs.docker.com/reference/cli/docker/container/

```
C:\Users\weick>docker container --help

Usage:  docker container COMMAND

Manage containers

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  exec        Execute a command in a running container
  export      Export a container's filesystem as a tar archive
  inspect     Display detailed information on one or more containers
  kill        Kill one or more running containers
  logs        Fetch the logs of a container
  ls          List containers
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  prune       Remove all stopped containers
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  run         Create and run a new container from an image
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker container COMMAND --help' for more information on a command.
```

## 容器运行常用命令
```
-a stdin: 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项
-d: 后台运行容器，并返回容器ID
-i: 以交互模式运行容器，通常与 -t 同时使用
-P: 随机端口映射，容器内部端口随机映射到主机的端口
-p: 指定端口映射，格式为：主机(宿主)端口:容器端口
-t: 为容器重新分配一个伪输入终端，通常与 -i 同时使用
--name="nginx-lb": 为容器指定一个名称
--dns 8.8.8.8: 指定容器使用的DNS服务器，默认和宿主一致
--dns-search example.com: 指定容器DNS搜索域名，默认和宿主一致
-h "mars": 指定容器的hostname
-e username="ritchie": 设置环境变量
--env-file=[]: 从指定文件读入环境变量
--cpuset="0-2" or --cpuset="0,1,2": 绑定容器到指定CPU运行
-m :设置容器使用内存最大值
--net="bridge": 指定容器的网络连接类型，支持 bridge/host/none/container: 四种类型
--link=[]: 添加链接到另一个容器
--expose=[]: 开放一个端口或一组端口
--volume , -v: 绑定一个卷
```
使用 docker run --help 查看更多信息

## 容器基本操作
| 操作 | 命令 |
| ------- | ------- |
|容器的创建|docker container run \<image name>|
|容器的列出(up)|docker container ls|
|容器的列出(up和exit)|docker container ls -a|
|容器的信息|docker inspect \<name or ID>|
|容器的特定信息|docker inspect --format='{{.NodeName.NodeName}}' \<name or ID>|
|容器的停止|docker container stop \<name or ID>|
|容器的删除|docker container rm \<name or ID>|

创建并运行容器例子：
```
C:\Users\weick>docker container run -d --publish 80:80 --name webhost nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
8a1e25ce7c4f: Pull complete
e78b137be355: Pull complete
39fc875bd2b2: Pull complete
035788421403: Pull complete
87c3fb37cbf2: Pull complete
c5cdd1ce752d: Pull complete
33952c599532: Pull complete
Digest: sha256:6db391d1c0cfb30588ba0bf72ea999404f2764febf0f1f196acd5867ac7efa7e
Status: Downloaded newer image for nginx:latest
01c810a2b68fdcf228c3368f211f5d5a0e4a6e07e8c9a8d6a96c7f5091b11e67
```
## 容器批量操作
```
docker container stop cd3 269 34b 751 //批量停止 Docker 容器
docker container stop $(docker container ps -aq) // 停止所有正在运行的 Docker 容器
docker container rm $(docker container ps -aq) // 删除所有正在运行的 Docker 容器
docker system prune -a -f // 可以快速对系统进行清理，删除停止的容器，不用的image，等等
```
$(...)：这个部分是 Bash 中的命令替换语法。它会将 docker container ps -aq （列出所有正在运行的容器的 ID）的输出作为参数传递给后面的命令。
官方文档：https://docs.docker.com/engine/reference/builder/

- Dockerfile是用于构建docker镜像的文件
- Dockerfile里包含了构建镜像所需的“指令”
- Dockerfile有其特定的语法规则

容器即进程，所以镜像就是一个运行这个进程所需要的环境。

一个Dockerfile的基本结构
```
FROM ubuntu:22.04
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y python3.10 python3-pip python3.10-dev
ADD hello.py /
CMD ["python3", "/hello.py"]
```
第一步：选择基础镜像
第二步：安装依赖和py的一些包
第三步：将本地py文件添加到镜像根目录
第四步：执行py

使用Dockerfile构建image
```
docker image build -f hello-dockerfile.txt -t hello-dockerfile .
```

使用Dockerfile构建image并运行容器过程
```
PS F:\MyDocker\DockerNote> docker image build -f hello-dockerfile.txt -t hello-dockerfile .
[+] Building 87.0s (8/8) FINISHED                                                                                                                                                                 docker:default 
 => [internal] load build definition from hello-dockerfile.txt                                                                                                                                              0.3s 
 => => transferring dockerfile: 254B                                                                                                                                                                        0.0s 
 => [internal] load metadata for docker.io/library/ubuntu:22.04                                                                                                                                             4.4s 
 => => transferring context: 2B                                                                                                                                                                             0.0s 
 => => resolve docker.io/library/ubuntu:22.04@sha256:77906da86b60585ce12215807090eb327e7386c8fafb5402369e421f44eff17e                                                                                       0.1s 
 => => transferring context: 56B                                                                                                                                                                            0.0s 
 => [2/3] RUN apt-get update &&     DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y python3.10 python3-pip python3.10-dev                                                        80.7s 
 => [3/3] ADD hello.py /                                                                                                                                                                                    0.1s 
 => exporting to image                                                                                                                                                                                      1.1s 
 => => exporting layers                                                                                                                                                                                     1.1s 
 => => writing image sha256:d3dbfcec836e9d4d07cb474ce01af12d895d318210499b6624a0ee2faeae4b52                                                                                                                0.0s 
 => => naming to docker.io/library/hello-dockerfile                                                                                                                                                         0.0s 

View build details: docker-desktop://dashboard/build/default/default/07vmwk6117q282qfe0uz4qrxa
PS F:\MyDocker\DockerNote> docker image ls
REPOSITORY         TAG       IMAGE ID       CREATED          SIZE
hello-dockerfile   latest    d3dbfcec836e   22 seconds ago   225MB
ubuntu             latest    ca2b0f26964c   3 weeks ago      77.9MB
nginx              latest    92b11f67642b   4 weeks ago      187MB
mysql              latest    019814493c7a   2 months ago     632MB
PS F:\MyDocker\DockerNote> docker run hello-dockerfile
hello docker
PS F:\MyDocker\DockerNote> docker container ls -a
CONTAINER ID   IMAGE              COMMAND                   CREATED              STATUS                          PORTS                NAMES
d07f868f305b   hello-dockerfile   "python3 /hello.py"       About a minute ago   Exited (0) About a minute ago                        frosty_lehmann
6fc95d84c1be   nginx              "/docker-entrypoint.…"   2 days ago           Exited (255) 38 hours ago       0.0.0.0:80->80/tcp   webhost
PS F:\MyDocker\DockerNote> 
```
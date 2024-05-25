往镜像里复制文件有两种方式，COPY 和 ADD。

**Dockerfile 中的 COPY 指令**用于将文件或目录从构建上下文中的指定位置复制到容器中的指定位置。它的基本语法如下：
```
COPY <源路径> <目标路径>
```
- <源路径>：构建上下文中的文件或目录的路径。这是相对于 Dockerfile 所在目录的路径。
- <目标路径>：容器中的目标路径，用于指定文件或目录复制到容器中的位置。

下面是一个简单的示例，演示了如何在 Dockerfile 中使用 COPY 指令：
```
FROM ubuntu:latest

# 将当前目录下的文件 "example.txt" 复制到容器中的 "/app" 目录下
COPY example.txt /app/

# 将当前目录下的目录 "src" 复制到容器中的 "/app" 目录下
COPY src /app/

```
在这个示例中，假设在 Dockerfile 所在的目录中存在一个名为 example.txt 的文件和一个名为 src 的目录。COPY example.txt /app/ 指令将 example.txt 文件复制到容器中的 /app/ 目录下，COPY src /app/ 指令将 src 目录复制到容器中的 /app/ 目录下。

需要注意的是，在使用 COPY 指令时，如果指定的路径是一个目录，Dockerfile 会复制该目录及其内容到容器中的目标路径。

**Dockerfile 中的 ADD 指令**与 COPY 指令类似，但它具有更多的功能。除了从构建上下文中的指定位置复制文件到容器中的指定位置之外，ADD 还可以处理远程 URL 和自动解压归档文件。然而，由于其功能较多，建议在大多数情况下优先使用 COPY 指令，因为它更简单并且在大多数情况下足够使用。

ADD 指令的基本语法如下：
```
ADD <源路径> <目标路径>
```
- <源路径>：构建上下文中的文件或目录的路径。这是相对于 Dockerfile 所在目录的路径。
- <目标路径>：容器中的目标路径，用于指定文件或目录复制到容器中的位置。

以下是一个示例，演示了如何在 Dockerfile 中使用 ADD 指令：
```
FROM ubuntu:latest

# 将当前目录下的文件 "example.txt" 复制到容器中的 "/app" 目录下
ADD example.txt /app/

# 将当前目录下的目录 "src" 复制到容器中的 "/app" 目录下
ADD src /app/

# 从 URL 下载文件到容器中的 "/downloads" 目录下
ADD http://example.com/file.zip /downloads/

# 将归档文件 "archive.tar.gz" 解压到容器中的 "/data" 目录下
ADD archive.tar.gz /data/
```

**Dockerfile 中的 WORKDIR 指令**用于设置在容器中执行命令时的工作目录。这个指令可以确保在容器中运行的命令相对于该目录执行，从而简化命令的书写，并且在构建和运行容器时提供了一致的环境。

以下是一个简单的 Dockerfile 示例，演示了如何使用 WORKDIR 指令：
```
FROM ubuntu:latest

# 设置工作目录为 /app
WORKDIR /app

# 复制当前目录下的所有文件到容器中的 /app 目录
COPY . .

# 执行一些命令，例如在 /app 目录下创建一个文件
RUN touch example.txt

# 在容器中执行命令时，默认将相对于 /app 目录
CMD ls -l
```

演示例子：
```
FROM ubuntu:latest

# 设置工作目录为 /app
WORKDIR /app

# 复制当前目录下的所有文件到容器中的 /app 目录
COPY hello.py .

# 将归档文件 "archive.tar.gz" 解压到容器中的 "/app/data" 目录下
ADD archive.tar.gz data/

# 执行一些命令，例如在 /app 目录下创建一个文件
RUN touch example.txt

# 在容器中执行命令时，默认将相对于 /app 目录
CMD ls -l
```
```
PS F:\MyDocker\DockerNote> docker build -f Dockerfile-copy -t dockerfile-copy .
[+] Building 0.7s (10/10) FINISHED                                                                                                                                                               docker:default 
 => [internal] load build definition from Dockerfile-copy                                                                                                                                                  0.0s 
 => => transferring dockerfile: 471B                                                                                                                                                                       0.0s 
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                                                                                           0.0s 
 => [internal] load .dockerignore                                                                                                                                                                          0.0s 
 => [1/5] FROM docker.io/library/ubuntu:latest                                                                                                                                                             0.0s 
 => [internal] load build context                                                                                                                                                                          0.0s 
 => => transferring context: 63B                                                                                                                                                                           0.0s 
 => CACHED [2/5] WORKDIR /app                                                                                                                                                                              0.0s 
 => CACHED [3/5] COPY hello.py .                                                                                                                                                                           0.0s 
 => [4/5] ADD archive.tar.gz data/                                                                                                                                                                         0.1s 
 => [5/5] RUN touch example.txt                                                                                                                                                                            0.3s 
 => => exporting layers                                                                                                                                                                                    0.1s 
 => => writing image sha256:17ec920eeea8be19b7f265687cdf791203d0f5ac6b60309b45d0ff90e964d17a                                                                                                               0.0s 
 => => naming to docker.io/library/dockerfile-copy                                                                                                                                                         0.0s 

View build details: docker-desktop://dashboard/build/default/default/tg1d521gdnt1a9i99izdft8ms

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview
PS F:\MyDocker\DockerNote> docker image ls
REPOSITORY             TAG       IMAGE ID       CREATED              SIZE
dockerfile-copy        latest    17ec920eeea8   About a minute ago   77.9MB
bad-dockerfile-image   latest    a56e13580600   24 hours ago         154MB
hello-dockerfile       latest    d3dbfcec836e   24 hours ago         225MB
ubuntu                 latest    ca2b0f26964c   3 weeks ago          77.9MB
nginx                  latest    92b11f67642b   5 weeks ago          187MB
mysql                  latest    019814493c7a   2 months ago         632MB
PS F:\MyDocker\DockerNote> docker image history 17e
IMAGE          CREATED              CREATED BY                                       SIZE      COMMENT
17ec920eeea8   About a minute ago   CMD ["/bin/sh" "-c" "ls -l"]                     0B        buildkit.dockerfile.v0
<missing>      About a minute ago   RUN /bin/sh -c touch example.txt # buildkit      0B        buildkit.dockerfile.v0
<missing>      About a minute ago   ADD archive.tar.gz data/ # buildkit              437B      buildkit.dockerfile.v0
<missing>      19 minutes ago       COPY hello.py . # buildkit                       21B       buildkit.dockerfile.v0
<missing>      19 minutes ago       WORKDIR /app                                     0B        buildkit.dockerfile.v0
<missing>      3 weeks ago          /bin/sh -c #(nop)  CMD ["/bin/bash"]             0B
<missing>      3 weeks ago          /bin/sh -c #(nop) ADD file:21c2e8d95909bec6f…   77.9MB
<missing>      3 weeks ago          /bin/sh -c #(nop)  LABEL org.opencontainers.…   0B
<missing>      3 weeks ago          /bin/sh -c #(nop)  LABEL org.opencontainers.…   0B
<missing>      3 weeks ago          /bin/sh -c #(nop)  ARG LAUNCHPAD_BUILD_ARCH      0B
<missing>      3 weeks ago          /bin/sh -c #(nop)  ARG RELEASE                   0B
PS F:\MyDocker\DockerNote> docker container run -it dockerfile-copy sh
# ls
data  example.txt  hello.py
# cd data
# ls
archive.tar.gz
# exit
```

因此在 COPY 和 ADD 指令中选择的时候，可以遵循这样的原则，所有的文件复制均使用 COPY 指令，仅在需要自动解压缩的场合使用 ADD。
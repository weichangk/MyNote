RUN 主要用于在Image里执行指令，比如安装软件，下载文件等。

如：
```
FROM ubuntu:20.04
RUN apt-get update
RUN apt-get install -y wget
RUN wget https://github.com/ipinfo/cli/releases/download/ipinfo-2.0.1/ipinfo_2.0.1_linux_amd64.tar.gz
RUN tar zxf ipinfo_2.0.1_linux_amd64.tar.gz
RUN mv ipinfo_2.0.1_linux_amd64 /usr/bin/ipinfo
RUN rm -rf ipinfo_2.0.1_linux_amd64.tar.gz
```

镜像的大小和分层
```
PS F:\MyDocker\DockerNote> docker image build -f bad-dockerfile.txt -t bad-dockerfile-image .
 => [internal] load build definition from bad-dockerfile.txt                                                                                                                                                0.0s 
 => => transferring dockerfile: 354B                                                                                                                                                                        0.0s 
 => [internal] load metadata for docker.io/library/ubuntu:20.04                                                                                                                                             4.4s 
 => [internal] load .dockerignore                                                                                                                                                                           0.0s 
 => => transferring context: 2B                                                                                                                                                                             0.0s 
 => [1/7] FROM docker.io/library/ubuntu:20.04@sha256:80ef4a44043dec4490506e6cc4289eeda2d106a70148b74b5ae91ee670e9c35d                                                                                       5.0s 
 => => resolve docker.io/library/ubuntu:20.04@sha256:80ef4a44043dec4490506e6cc4289eeda2d106a70148b74b5ae91ee670e9c35d                                                                                       0.0s 
 => => sha256:80ef4a44043dec4490506e6cc4289eeda2d106a70148b74b5ae91ee670e9c35d 1.13kB / 1.13kB                                                                                                              0.0s 
 => => sha256:48c35f3de33487442af224ed4aabac19fd9bfbd91ee90e9471d412706b20ba73 424B / 424B                                                                                                                  0.0s 
 => => sha256:3cff1c6ff37e0101a08119d0743ba95c7f505d00298f5a169129e4e9086cde9e 2.29kB / 2.29kB                                                                                                              0.0s 
 => => sha256:17d0386c2fff30a5b92652bbef2b84639dba9b9f17bdbb819c8d10badd827fdb 27.51MB / 27.51MB                                                                                                            3.1s 
 => => extracting sha256:17d0386c2fff30a5b92652bbef2b84639dba9b9f17bdbb819c8d10badd827fdb                                                                                                                   1.6s 
 => [2/7] RUN apt-get update                                                                                                                                                                               21.6s 
 => [3/7] RUN apt-get install -y wget                                                                                                                                                                      12.8s 
 => [4/7] RUN wget https://github.com/ipinfo/cli/releases/download/ipinfo-2.0.1/ipinfo_2.0.1_linux_amd64.tar.gz                                                                                             3.9s 
 => [5/7] RUN tar zxf ipinfo_2.0.1_linux_amd64.tar.gz                                                                                                                                                       0.6s 
 => [6/7] RUN mv ipinfo_2.0.1_linux_amd64 /usr/bin/ipinfo                                                                                                                                                   0.5s 
 => [7/7] RUN rm -rf ipinfo_2.0.1_linux_amd64.tar.gz                                                                                                                                                        0.5s 
 => exporting to image                                                                                                                                                                                      0.5s 
 => => exporting layers                                                                                                                                                                                     0.4s 
 => => writing image sha256:a56e135806006509c16fa4bfa87030ca7b061d2ec8e66f1bd5d536f002a8509f                                                                                                                0.0s 
 => => naming to docker.io/library/bad-dockerfile-image                                                                                                                                                     0.0s 

View build details: docker-desktop://dashboard/build/default/default/nt47bzeaqr16r51a6m0ndwsf7
PS F:\MyDocker\DockerNote> docker image ls
REPOSITORY             TAG       IMAGE ID       CREATED          SIZE
bad-dockerfile-image   latest    a56e13580600   47 seconds ago   154MB
hello-dockerfile       latest    d3dbfcec836e   14 minutes ago   225MB
ubuntu                 latest    ca2b0f26964c   3 weeks ago      77.9MB
nginx                  latest    92b11f67642b   4 weeks ago      187MB
mysql                  latest    019814493c7a   2 months ago     632MB
PS F:\MyDocker\DockerNote> docker image history a56
IMAGE          CREATED              CREATED BY                                       SIZE      COMMENT
a56e13580600   About a minute ago   RUN /bin/sh -c rm -rf ipinfo_2.0.1_linux_amd…   0B        buildkit.dockerfile.v0
<missing>      About a minute ago   RUN /bin/sh -c mv ipinfo_2.0.1_linux_amd64 /…   9.36MB    buildkit.dockerfile.v0
<missing>      About a minute ago   RUN /bin/sh -c tar zxf ipinfo_2.0.1_linux_am…   9.36MB    buildkit.dockerfile.v0
<missing>      About a minute ago   RUN /bin/sh -c wget https://github.com/ipinf…   4.85MB    buildkit.dockerfile.v0
<missing>      About a minute ago   RUN /bin/sh -c apt-get install -y wget # bui…   7.63MB    buildkit.dockerfile.v0
<missing>      About a minute ago   RUN /bin/sh -c apt-get update # buildkit         49.9MB    buildkit.dockerfile.v0
<missing>      4 weeks ago          /bin/sh -c #(nop)  CMD ["/bin/bash"]             0B
<missing>      4 weeks ago          /bin/sh -c #(nop) ADD file:a25798f31219000d6…   72.8MB
<missing>      4 weeks ago          /bin/sh -c #(nop)  LABEL org.opencontainers.…   0B
<missing>      4 weeks ago          /bin/sh -c #(nop)  LABEL org.opencontainers.…   0B
<missing>      4 weeks ago          /bin/sh -c #(nop)  ARG LAUNCHPAD_BUILD_ARCH      0B
<missing>      4 weeks ago          /bin/sh -c #(nop)  ARG RELEASE                   0B
PS F:\MyDocker\DockerNote> 
```

每一行的RUN命令都会产生一层image layer, 导致镜像的臃肿

改进Dockerfile
```
FROM ubuntu:20.04
RUN apt-get update && \
    apt-get install -y wget && \
    wget https://github.com/ipinfo/cli/releases/download/ipinfo-2.0.1/ipinfo_2.0.1_linux_amd64.tar.gz && \
    tar zxf ipinfo_2.0.1_linux_amd64.tar.gz && \
    mv ipinfo_2.0.1_linux_amd64 /usr/bin/ipinfo && \
    rm -rf ipinfo_2.0.1_linux_amd64.tar.gz
```
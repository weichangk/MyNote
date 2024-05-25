要导出 Docker 镜像，你可以使用 docker save 命令。这个命令会将一个或多个镜像打包成一个 tar 归档文件。

```
// 把 my_image 镜像保存为 my_image.tar 文件
docker save -o my_image.tar my_image
```

要导入 Docker 镜像，你可以使用 docker load 命令。这个命令会从一个 tar 归档文件中加载镜像。
```
// 将 my_image.tar 文件中的镜像加载到 Docker 中
docker load -i my_image.tar
```


```
// 导出镜像文件
C:\Users\weick>docker image save -o my_ubuntu.tar ubuntu

// 查看导出文件
C:\Users\weick>dir /b
my_ubuntu.tar

C:\Users\weick>docker image rm ubuntu
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:77906da86b60585ce12215807090eb327e7386c8fafb5402369e421f44eff17e
Deleted: sha256:ca2b0f26964cf2e80ba3e084d5983dab293fdb87485dc6445f3f7bbfc89d7459
Deleted: sha256:5498e8c22f6996f25ef193ee58617d5b37e2a96decf22e72de13c3b34e147591

C:\Users\weick>docker image ls
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
nginx        latest    92b11f67642b   4 weeks ago    187MB
mysql        latest    019814493c7a   2 months ago   632MB

// 导入镜像
C:\Users\weick>docker load -i my_ubuntu.tar
5498e8c22f69: Loading layer [==================================================>]  80.41MB/80.41MB
Loaded image: ubuntu:latest

C:\Users\weick>docker image ls
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
ubuntu       latest    ca2b0f26964c   2 weeks ago    77.9MB
nginx        latest    92b11f67642b   4 weeks ago    187MB
mysql        latest    019814493c7a   2 months ago   632MB

C:\Users\weick>
```
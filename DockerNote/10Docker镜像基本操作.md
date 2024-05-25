**docker image** 查看 image 相关命令
```
C:\Users\weick>docker image

Usage:  docker image COMMAND

Manage images

Commands:
  build       Build an image from a Dockerfile
  history     Show the history of an image
  import      Import the contents from a tarball to create a filesystem image
  inspect     Display detailed information on one or more images
  load        Load an image from a tar archive or STDIN
  ls          List images
  prune       Remove unused images
  pull        Download an image from a registry
  push        Upload an image to a registry
  rm          Remove one or more images
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

Run 'docker image COMMAND --help' for more information on a command.

C:\Users\weick>
```

搜索 Docker Hub 上的 MySQL 镜像并查看它们的标签和版本信息 **docker search mysql**
```
C:\Users\weick>docker search mysql
NAME                            DESCRIPTION                                      STARS     OFFICIAL
mysql                           MySQL is a widely used, open-source relation…   14941     [OK]
mariadb                         MariaDB Server is a high performing open sou…   5703      [OK]
percona                         Percona Server is a fork of the MySQL relati…   626       [OK]
phpmyadmin                      phpMyAdmin - A web interface for MySQL and M…   959       [OK]
bitnami/mysql                   Bitnami MySQL Docker Image                       110
bitnami/mysqld-exporter                                                          6
cimg/mysql                                                                       3
ubuntu/mysql                    MySQL open source fast, stable, multi-thread…   61
rapidfort/mysql                 RapidFort optimized, hardened image for MySQL    25
rapidfort/mysql8-ib             RapidFort optimized, hardened image for MySQ…   9
google/mysql                    MySQL server for Google Compute Engine           25
elestio/mysql                   Mysql, verified and packaged by Elestio          0
rapidfort/mysql-official        RapidFort optimized, hardened image for MySQ…   9
bitnamicharts/mysql                                                              0
hashicorp/mysql-portworx-demo                                                    0
databack/mysql-backup           Back up mysql databases to... anywhere!          111
linuxserver/mysql               A Mysql container, brought to you by LinuxSe…   41
mirantis/mysql                                                                   0
docksal/mysql                   MySQL service images for Docksal - https://d…   0
linuxserver/mysql-workbench                                                      55
vitess/mysqlctld                vitess/mysqlctld                                 1
eclipse/mysql                   Mysql 5.7, curl, rsync                           1
drupalci/mysql-5.5              https://www.drupal.org/project/drupalci          3
drupalci/mysql-5.7              https://www.drupal.org/project/drupalci          0
datajoint/mysql                 MySQL image pre-configured to work smoothly …   2
```
镜像的拉取 Pull Image 默认从Docker Hub拉取，如果不指定版本，会拉取最新版 **docker image pull masql**
```
C:\Users\weick>docker image pull masql
Using default tag: latest
9a5c778f631f: Pull complete
Digest: sha256:9d1c923e5f66a89607285ee2641f8a53430a1ccd5e4a62b35eb8a48b74b9ff48     721B/883B
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest

C:\Users\weick>docker image ls
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
ubuntu       latest    ca2b0f26964c   2 weeks ago    77.9MB
nginx        latest    92b11f67642b   4 weeks ago    187MB
mysql        latest    019814493c7a   2 months ago   632MB

C:\Users\weick>

```

拉取指定版本 **image pull mysql:5.7**
```
C:\Users\weick>docker image pull mysql:5.7
5.7: Pulling from library/mysql
20e4dcae4c69: Pull complete
Digest: sha256:4bc6bc963e6d8443453676cae56536f4b8156d78bae03c0145cbe47c2aad73bb
Status: Downloaded newer image for mysql:5.7
docker.io/library/mysql:5.7
```

删除镜像 **docker image rm 510**
```
C:\Users\weick>docker image rm 510
Untagged: mysql:5.7
Untagged: mysql@sha256:4bc6bc963e6d8443453676cae56536f4b8156d78bae03c0145cbe47c2aad73bb
Deleted: sha256:5107333e08a87b836d48ff7528b1e84b9c86781cc9f1748bbc1b8c42a870d933
Deleted: sha256:37fd5f1492d4e9cb540c52c26655f220568050438f804275e886200c8807ffb4
Deleted: sha256:1105a50d3483cb9f970e70cf5163e3352f0b2fe2ff07c6abcca6f34228e76dc5
Deleted: sha256:94187496c18bb11b78e71017f2774ad3c0a734da9749a46e917c4239504e9322
Deleted: sha256:ae59716eae3be604a4fd43e86fd2ad504cb06c89cc064c73c78eee651e675805
Deleted: sha256:97d26ca29ec287ff4bd09a49602c44cbcabcf3303ddc726b3b94cbe26dfe1c94
Deleted: sha256:27303974d12144264b32b8936ca7c90d72bdba939a9e791010201b3b1717c4c4
Deleted: sha256:4d4483f06dbe01282c10cb9e429a0be826c18c61048f7860dad49ae7f6bac927
Deleted: sha256:3b73a6f6b3298c568dcfb8fa5e96c581a1b5c0ad395b0c38f9addd0c79703124
Deleted: sha256:46446bf265a411a4a13a4adc86f60c9e0479a2e03273c98cafab7bc4151dd2bc
Deleted: sha256:1d5264146b09a27a8fc6801dc239a4962582ed27dd2fbd8ee708463a1857b06b
Deleted: sha256:cff044e186247f93aa52554c96d77143cc92f99b2b55914038d0941fddeb6623
```
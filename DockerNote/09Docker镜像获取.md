- pull from registry (online) 从registry拉取
    - public（公有）
    - private（私有）
- build from Dockerfile (online) 从Dockerfile构建
- load from file (offline) 文件导入 （离线）

![](img/docker-stages.png)

基础镜像选择（from）基本原则
- 官方镜像优于非官方的镜像，如果没有官方镜像，则尽量选择Dockerfile开源的
- 固定版本tag而不是每次都使用latest
- 尽量选择体积小的镜像
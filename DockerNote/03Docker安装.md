## 在 Windows 系统上安装 Docker
安装官方教程：https://docs.docker.com/desktop/install/windows-install/


因为要开启虚拟化服务，所以使用windows操作系统至少要windows10专业版，在windows操作系统中虚拟化服务叫Hyper-V，在安装和运行dockre之前要确保windows功能Hyper-V是开启状态。

如果安装后提示需要 WSL2 Linux 内核更新，可参考：https://docs.microsoft.com/zh-cn/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package 下载最新包：适用于 x64 计算机的 WSL2 Linux 内核更新包，安装更新包后，restart docker即可。

**配置镜像加速器**
参考：https://www.runoob.com/docker/docker-mirror-acceleration.html

配置路径 C:\Users\xxxx\.docker\daemon.json
添加配置 "registry-mirrors":["https://docker.mirrors.ustc.edu.cn"]

国内加速器服务：
Docker 官方中国区：https://registry.docker-cn.com
网易：http://hub-mirror.c.163.com
中国科技大学：https://docker.mirrors.ustc.edu.cn
阿里云：https://<你的ID>.mirror.aliyuncs.com

## 在 Linux 系统上安装 Docker
待补充
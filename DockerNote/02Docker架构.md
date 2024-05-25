Docker 官方介绍：https://docs.docker.com/get-started/overview/

![](img/docker-architecture.webp)

Docker 的架构是一个典型的客户端-服务器架构，包括以下几个核心组件：

- **Docker Daemon（dockerd）**：
Docker 守护进程，运行在宿主机上，负责管理 Docker 对象，如镜像、容器、网络和存储卷。它接收来自 Docker 客户端的请求，并通过 Docker API 与其他组件通信。

- **Docker Client**：
Docker 客户端是用户与 Docker 守护进程交互的主要方式。用户可以使用命令行工具（如 docker 命令）或 Docker API 与 Docker 守护进程通信，发送操作指令，如创建、启动、停止或删除容器等。

- **Docker 镜像（Docker Images）**：
Docker 镜像是用于创建 Docker 容器的只读模板。它包含了运行容器所需的文件系统、代码、运行时和其他依赖项。镜像可以从 Docker Hub 或其他镜像仓库拉取，也可以通过 Dockerfile 构建。

- **Docker 容器（Docker Containers）**：
Docker 容器是 Docker 镜像的实例化运行时对象。每个容器都是独立的、隔离的运行环境，包含了运行特定应用程序所需的一切。Docker 容器可以快速创建、启动、停止和删除，具有轻量级、可移植性和隔离性等特点。

- **Docker Registry**：
Docker 注册表是存储 Docker 镜像的仓库，用于集中管理和分发镜像。Docker Hub 是 Docker 官方提供的公共注册表，用户可以在其中找到大量的官方和社区维护的镜像。除了 Docker Hub 外，还可以搭建私有的 Docker Registry，用于组织内部镜像的存储和分享。

通过这些核心组件，Docker 实现了一个简单而强大的容器化平台，使得开发人员和运维人员可以更加便捷地构建、部署和管理应用程序。
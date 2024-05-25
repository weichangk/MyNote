Docker是client-server架构，理论上Client和Server可以不在一台机器上。在构建docker镜像的时候，需要把所需要的文件由CLI（client）发给Server，这些文件实际上就是build context

.dockerignore 是 Docker 中用来忽略不需要包含在镜像中的文件或目录的配置文件。类似于 .gitignore 文件，它指定了 Docker 在构建镜像时应该忽略哪些文件或目录。

.dockerignore 文件中的规则可以与 .gitignore 文件中的规则相同，因为 Docker 会使用 Go 语言的 filepath.Match 匹配模式。
CMD可以用来设置容器启动时默认会执行的命令。

- 容器启动时默认执行的命令
- 如果docker container run启动容器时指定了其它命令，则CMD命令会被忽略
- 如果定义了多个CMD，只有最后一个会被执行

CMD 指令有两种形式：shell 形式和 exec 形式。

在 shell 形式中，CMD 指令使用字符串格式。例如：
```
CMD echo "Hello, world!"
```
在这个示例中，容器启动时将会执行 echo "Hello, world!" 这个命令。

在 exec 形式中，CMD 指令使用 JSON 数组格式。例如：
```
CMD ["echo", "Hello, world!"]
```
同样也是执行 echo "Hello, world!" 这个命令，但是命令以数组的形式提供，不再经过 shell 解释，因此避免了一些潜在的问题。

通常情况下，推荐使用 exec 形式的 CMD，因为它可以避免与 shell 相关的一些问题，例如字符转义、参数解析等。另外，如果希望执行的命令包含空格或其他特殊字符，使用 exec 形式可以更清晰地指定参数。
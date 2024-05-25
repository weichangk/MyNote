ENTRYPOINT 也可以设置容器启动时要执行的命令，但是和CMD是有区别的。

- CMD 设置的命令，可以在docker container run 时传入其它命令，覆盖掉 CMD 的命令，但是 ENTRYPOINT 所设置的命令是一定会被执行的
- ENTRYPOINT 和 CMD 可以联合使用，ENTRYPOINT 设置执行的命令，CMD传递参数

```
FROM ubuntu:20.04
CMD ["echo", "hello docker"]
```
把上面的Dockerfile build成一个叫 demo-cmd 的镜象

```
FROM ubuntu:20.04
ENTRYPOINT ["echo", "hello docker"]
```
把上面的Dockerfile build成一个叫 demo-entrypoint 的镜象

CMD的镜像，如果执行创建容器，不指定运行时的命令，则会默认执行CMD所定义的命令，打印出 hello docker
```
$ docker container run -it --rm demo-cmd
hello docker
```

但是如果我们docker container run的时候指定命令，则该命令会覆盖掉CMD的命令，打印出 hello world，如：
```
$ docker container run -it --rm demo-cmd echo "hello world"
hello world
```

但是ENTRYPOINT的容器里ENTRYPOINT所定义的命令则无法覆盖，一定会执行
```
$ docker container run -it --rm demo-entrypoint
hello docker
$ docker container run -it --rm demo-entrypoint echo "hello world"
hello docker echo hello world
$
```
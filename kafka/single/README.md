# kafka

# 挂载问题

目前挂载的内容不在当前目录中,而是在Docker Volume中

```shell
# 列出所有的卷
docker volume ls
# 查看卷的数据 里面的Mountpoint属性则为宿主机的目录(不知为何的没有这个目录找不到这个文件)
docker volume inpect kafka_sksingle-kmultiple_zoo1-log
```

# 错误

1. 提示挂载文件错误则分别创建zookeeper目录在次执行即可

# 参考

https://github.com/conduktor/kafka-stack-docker-compose
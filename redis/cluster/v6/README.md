# redis

搭建集群模式3主3从模式,登录账号root

# 镜像

镜像拉取对应的版本根据实际情况进行修改调整,可查看支持的镜像版本

https://hub.docker.com/_/redis/tags

拉取正常最新版本

```shell
docker pull redis:latest
```

拉取alpine版本,此版本镜像内容很小

```shell
docker pull redis:5.0.14-alpine
```

# 配置

redis不同版本有不同的配置,因此在实际使用当中根据自己的情况进行调整,不同版本的配置下载地址：
https://download.redis.io/releases/
下载对应版本之后解压redis-x.x.x.tar.gz文件,在根目录中有`redis.conf`文件,直接拷贝到当前项目目录即可

另外配置中需要更改绑定方式,详情看配置文件中的标注,以下是针对6.2.7版本配置文件

- protected-mode 98行左右
- daemonize 263行左右
- masterauth 490行左右
- requirepass 907行左右
- cluster-enabled 1391行左右
- cluster-config-file 1399行左右
- cluster-node-timeout 1409行左右
- cluster-announce-port 1561行左右
- cluster-announce-bus-port 1562行左右

# 问提

### 1.哪些节点是主节点哪些是从节点？

默认情况下启动主从节点是随机不固定自动分配的,等需要服务启动之后才能确定节点关系,可使用命令行查看集群先关信息:

```shell
./redis-cli --cluster check 127.0.0.0:
```

或者进入命令行之后执行以下命令

```shell
cluster nodes
```

如果想更改关系可参考以下：
https://blog.csdn.net/guotianqing/article/details/119778684

### 2.Waiting for the cluster to join ......

原因是没有配置`cluster-announce-bus-port`端口,需要再配置文件中增加端口

### 3.(error) MOVED 15692 192.168.0.3:6379

原因是redis连接的时候没有指定集群模式只需要在原有链接的基础上加上 -c即可

```shell
./redis-cli -c -a root
```

### 4. 添加集群命令中`--cluster-replicas 1`得作用

相当于指定从节点有几个,比如我搭建了6个节点,--cluster-replicas设置为1时,则其中三个作为主节点,三个作为从节点。如果设置为0则代表6点节点都是主节点。

# 参考

https://zhuanlan.zhihu.com/p/551670740
https://www.cnblogs.com/tanghaorong/p/14339880.html
https://www.cnblogs.com/AD-milk/p/16200539.html
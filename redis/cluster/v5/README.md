# redis v5

未实现

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

另外配置中需要更改绑定方式,详情看配置文件中的标注
# ElasticSearch

本仓库基于8.10.1版本

# 命令

### 1. 重置enrollment-token用于浏览器使用

```shell
$ docker exec -it <imagename/imageid> /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
WARNING: Owner of file [/usr/share/elasticsearch/config/users] used to be [root], but now is [elasticsearch]
WARNING: Owner of file [/usr/share/elasticsearch/config/users_roles] used to be [root], but now is [elasticsearch]
eyJ2ZXIiOiI4LjEwLjEiLCJhZHIiOlsiMTkyLjE2OC45Ni4yOjkyMDAiXSwiZmdyIjoiN2Q3MzBiZjQ4ZjIyZjgwN2RkNzM2YzZmYzE5YThmODI3ZGE2YzEwNWY0NTNhZjkzZjhmOGUxMjNlNjg2N2I2NSIsImtleSI6IlRtYmxzWW9CU2FVZnp6RDRsQUFwOnJjT0h5UllfUnp1XzJSVFNoOGNHQmcifQ==
```

# 问题

### 1. 终端没有输出相关账号密码

在使用docker-compose方式运行时没有出现密码日志,打印日志如下:

```text
2023-09-20 14:43:51 {"@timestamp":"2023-09-20T06:43:51.093Z", "log.level": "INFO", "message":"Auto-configuration will not generate a password for the elastic built-in superuser, as we cannot  determine if there is a terminal attached to the elasticsearch process. You can use the `bin/elasticsearch-reset-password` tool to set the password for the elastic user.", "ecs.version": "1.2.0","service.name":"ES_ECS","event.dataset":"elasticsearch.server","process.thread.name":"main","log.logger":"org.elasticsearch.xpack.security.InitialNodeSecurityAutoConfiguration","elasticsearch.node.name":"3fe55ec41afe","elasticsearch.cluster.name":"docker-cluster"}
```

其含义是自动配置时无法为内置的 elastic 超级用户生成随机密码,因为无法判断 ElasticSearch 进程是否有终端连接。

解决方式：

1. 如果使用docker-compose则直接设置环境变量,比如:`ELASTIC_PASSWORD`
2. 使用命令行文件重置密码,会在命令行打印输出密码信息。

```shell
$ docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
$ docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```

检测密码是否正确：

```shell
$ curl --insecure --user elastic:password https://localhost:9200
{
  "name": "3fe55ec41afe",
  "cluster_name": "docker-cluster",
  "cluster_uuid": "UwllLlTbR4W38UqCYqCi8w",
  "version": {
    "number": "8.10.1",
    "build_flavor": "default",
    "build_type": "docker",
    "build_hash": "a94744f97522b2b7ee8b5dc13be7ee11082b8d6b",
    "build_date": "2023-09-14T20:16:27.027355296Z",
    "build_snapshot": false,
    "lucene_version": "9.7.0",
    "minimum_wire_compatibility_version": "7.17.0",
    "minimum_index_compatibility_version": "7.0.0"
  },
  "tagline": "You Know, for Search"
}
```
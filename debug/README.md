# Debug调试指南

## 一、安装Podman(或Docker)
- Ubuntu安装Podman
```
sudo apt-get install podman
```

> 备注1：推荐安装 podman 3.4.4 或以上。

## 二、拉取最小化容器进行测试

以官方提供的hello-world容器为例:
```
podman pull docker.io/hello-world
podman images
```

查看images:
```
$ podman images
REPOSITORY                     TAG         IMAGE ID      CREATED        SIZE
docker.io/library/hello-world  latest      d2c94e258dcb  11 months ago  27.4 kB
```

运行hello-world容器:
```
podman run --rm hello-world
```

> 备注：指定`--rm`选项，容器运行完毕时自动删除。


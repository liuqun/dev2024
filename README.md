# Example using podman/docker:

## Redis 配置
```
export REDIS_VERSION="7.2.4"
podman pull docker.io/redis:${REDIS_VERSION}

# 启动
podman run -d --rm \
    -p "6379:6379" \
    --name myredis \
    redis:${REDIS_VERSION}

##以下三行指定目录暂未启用, 此处仅留作备用选项
# export TOP_DIR=`pwd`
# export REDIS_DIR=${TOP_DIR}/redis
# export REDIS_LOG_DIR=${TOP_DIR}/redis-log
```

## Nginx
- To start my nginx server:
```
export MYDIR=`pwd`

# webpages
# nginx-log
# nginx-conf.d

export NGINX_VERSION="1.25.4"
podman pull docker.io/nginx:${NGINX_VERSION}
podman run -d --rm \
    -p 8080:80 \
    --name mynginx \
    -v $MYDIR/webpages:/usr/share/nginx/html:ro \
    -v $MYDIR/nginx-log:/var/log/nginx \
    nginx:${NGINX_VERSION}
```

> NOTE:
> The option `--rm` will automatically remove the nginx server instance after I stop it.

- To stop/delete my nginx server instance:

```
podman stop mynginx
```


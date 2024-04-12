# Example using podman/docker:

```
export MYDIR=/home/liuqun

# webpages
# nginx-log
# nginx-conf.d

podman run -d \
    -p 8080:80 \
    --name mynginx \
    -v $MYDIR/webpages:/usr/share/nginx/html \
    -v $MYDIR/nginx-log:/var/log/nginx \
    nginx
```


# Example using podman/docker:

- To start my nginx server:
```
export MYDIR=`pwd`

# webpages
# nginx-log
# nginx-conf.d

podman run -d --rm \
    -p 8080:80 \
    --name mynginx \
    -v $MYDIR/webpages:/usr/share/nginx/html \
    -v $MYDIR/nginx-log:/var/log/nginx \
    nginx
```

> NOTE:
> The option `--rm` will automatically remove the nginx server instance after I stop it.

- To stop/delete my nginx server instance:

```
podman stop mynginx
```


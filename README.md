# Example using podman/docker:

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
    -p "8080:80" \
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


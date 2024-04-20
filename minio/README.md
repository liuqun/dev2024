# MinIO

- Download image and run:

```
export MINIO_VERSION="RELEASE.2024-04-18T19-09-19Z"
podman pull docker.io/minio/minio:${MINIO_VERSION}

# Configure environment variables and start the MinIO server:
export MINIO_DIR=`pwd`
export MINIO_DATA_DIR=${MINIO_DIR}/data
export MINIO_ROOT_USER="foobar"
export MINIO_ROOT_PASSWORD="P@ssw0rd"
export MINIO_COMPRESS="off"
export MINIO_COMPRESS_EXTENSIONS=""
export MINIO_COMPRESS_MIME_TYPES=""
export TZ="Asia/Shanghai"

#
podman run -d --rm \
    -p "9000:9000" \
    -p "9001:9001" \
    -v ${MINIO_DIR}/data:/data \
    -v ${MINIO_DIR}/conf:/root/.minio/ \
    -e TZ=${TZ} \
    -e MINIO_DATA_DIR=/data \
    -e MINIO_ROOT_USER=${MINIO_ROOT_USER} \
    -e MINIO_ROOT_PASSWORD=${MINIO_ROOT_PASSWORD} \
    -e MINIO_COMPRESS=${MINIO_COMPRESS} \
    -e MINIO_COMPRESS_EXTENSIONS=${MINIO_COMPRESS_EXTENSIONS} \
    -e MINIO_COMPRESS_MIME_TYPES=${MINIO_COMPRESS_MIME_TYPES} \
    --name myminio \
    minio/minio:${MINIO_VERSION} \
    server /data --console-address ":9001"
```

## 访问 MinIO 控制台网页
打开本机`http://localhost:9001`端口，输入用户名foobar密码P@ssw0rd


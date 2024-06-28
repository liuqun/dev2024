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

### 创建任意存储桶
例如创建一个名为app的存储桶
### 添加用户并创建AccessKey
MinIO控制台网页生成的密钥文件: credentials.json
格式如下：
```
{
  "url":"http://127.0.0.1:9000",
  "accessKey":"vncGuydamGEZICablflV",
  "secretKey":"e8BIb6tXS6RIADwFCoNFKmuBfJsXr2RWGdjNG4md",
  "api":"s3v4",
  "path":"auto"
}
```

## 然后映射MinIO存储桶到Linux本地文件系统
参考资料
1. https://github.com/s3fs-fuse/s3fs-fuse
2. https://www.cnblogs.com/rongfengliang/p/10790072.html
```
# Ubuntu/Debian:
sudo apt-get install s3fs
# CentOS7: yum install -y s3fs-fuse
```

```
echo "foobar:P@ssw0rd" > passwd-s3fs
chmod 600 passwd-s3fs

# 创建挂载点
mkdir ~/bucket-app
s3fs -o passwd_file=passwd-s3fs \
    -o use_path_request_style \
    -o endpoint=us-east-1 \
    -o url=http://localhost:9000 \
    -o bucket=app ~/bucket-app
```

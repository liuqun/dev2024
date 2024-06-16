# 命令行客户端工具 mc
```
wget https://dl.min.io/client/mc/release/linux-amd64/mc
chomd 755 ./mc
```

credentials.json 文件可用 MinIO client 命令 mc 导入
```
mc alias import newalias ./credentials.json
```

导入后, 用户根目录的
    ~/.mc/config.json
文件中会记录 accessKey 和 secretKey 的值。
之后在使用 mc 命令查看 bucket 存储桶的内容时不用输入密码:
```
mc list newalias
```

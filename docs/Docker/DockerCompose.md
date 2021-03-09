## 安装 (Ubuntu)
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
```
sudo chmod +x /usr/local/bin/docker-compose
```
## 常用命令
创建工作目录并赋权限
```
mkdir /usr/local/docker/nginx && chown -R 200 /usr/local/docker/nginx
```

在 docker 目录下启动 docker
```
docker-compose up -d
```
查看 docker 运行
```
docker-compose ps
```
重启 docker
```
docker-compose restart
```
赋予权限
```
chmod 777 /
```
进入容器
```
sudo docker exec -it 0841c3225711 /bin/bash
```

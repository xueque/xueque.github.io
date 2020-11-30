{docsify-updated}
# Nginx Docker

##### docker-compose.yml


```yaml
version: '3.1'
services:
  nginx:
    restart: always
    image: nginx
    container_name: nginx-dashboard
    ports:

      - 80:80
            - 443:443
        volumes:
            - ./conf/conf.d/:/etc/nginx/conf.d/
                  - ./html/:/usr/share/nginx/html/
                  - ./logs/:/var/log/nginx/
environment:
  - TZ=Asia/Shanghai
```

##### nginx\conf\ nginx.conf

```shell
# nginx.conf 例：
user  root;
worker_processes  1;
 
error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;
 
 
events {
    worker_connections  1024;
}
 
 
http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;
    client_max_body_size 1024m;
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
 
    access_log  /var/log/nginx/access.log  main;
 
    sendfile        on;
    #tcp_nopush     on;
 
    keepalive_timeout  65;
 
    #gzip  on;
 
    include /etc/nginx/conf.d/*.conf;
}

```

##### nginx\conf\conf.d\default.conf

```shell
# default.conf 例：
server {
    listen       80;
    server_name  localhost;
	location = /uploadImage {
		proxy_pass http://192.168.0.172:8888/api/1/upload;
	}
	
    location / {
      root   /usr/share/nginx/html/dist;
	  try_files $uri $uri/ /index.html;		#解决vue的路由在nginx中刷新出现404
      index  index.html index.htm;
    }        
#	 location ~ /oss/ {
#      proxy_pass http://192.168.0.172:8888;
#    }
	
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html/dist;
    }
	location = /report.html {
        root   /usr/share/nginx/html/dist;
    }
	
}
```


    
`测试环境:树莓派-4b UbuntuServer 64-bit`   
   
# 安装   
```shell
# 检查版本
python3 -V
# 更新 apt-get
sudo apt-get update
# 安装 pip3
sudo apt-get install -y python3-pip
# 更新 pip
pip install --upgrade pip
sudo pip --version
# 安装环境
apt-get install libffi-dev
# 安装 docker-compose
sudo pip3 install docker-compose
sudo chmod +x /usr/local/bin/docker-compose
# 校验
docker-compose version
```
# mysql
```yaml
# 创建目录脚本
# mkdir -p /usr/local/docker/mysql/{mysql-data,conf.d,docker-entrypoint-initdb.d} && chmod -R 777  /usr/local/docker/mysql/ && cd /usr/local/docker/mysql/
# 
# docker-compose up -d
# docker-compose down
# docker-compose restart
version: "3"
services: 
  mysql:
    restart: always
    image: biarms/mysql:5.7
    # image: mysql:5.7
    container_name: mysql
    environment:
      - TZ=Asia/Shanghai
      - MYSQL_ROOT_PASSWORD=password
    # 设置数据库字符集
    command:
      --character-set-server=utf8mb4
      --collation-server=utf8mb4_general_ci
      # --lower_case_table_names=1
      # --explicit_defaults_for_timestamp=true
    ports: 
      - 3306:3306
    volumes: 
    # 使用相对路径
      - ./mysql-data:/var/lib/mysql
      - ./conf.d:/etc/mysql/conf.d
    # 只有在 mysql-data 为空,该目录下的 sql 脚本才会被执行,测试发现 插入数据 必须跟在对应表的后面,且只能 创建一个库
      - ./docker-entrypoint-initdb.d:/docker-entrypoint-initdb.d

  # adminer:
    # image: adminer:4.7.1
    # container_name: adminer
    # restart: always
    # ports: 
      # - 9000:8080
```
# nacos
```yaml
# 创建目录脚本
# mkdir -p /usr/local/docker/nacos/{logs,init.d} && chmod -R 777 /usr/local/docker/nacos/ && cd /usr/local/docker/nacos/
# 
# docker-compose up -d
# docker-compose down
# docker-compose restart
version: "3"
services:
  nacos:
    image: registry.cn-beijing.aliyuncs.com/xueque/nacos:2.0.1
    container_name: nacos-standalone-mysql
    environment:
      - TZ=Asia/Shanghai
      - PREFER_HOST_MODE=hostname
      - MODE=standalone
      - SPRING_DATASOURCE_PLATFORM=mysql
      - MYSQL_SERVICE_HOST=mysql
      - MYSQL_SERVICE_DB_NAME=nacos_config
      - MYSQL_SERVICE_PORT=3306
      - MYSQL_SERVICE_USER=root
      - MYSQL_SERVICE_PASSWORD=password
    volumes:
      - ./logs/:/home/nacos/logs
      - ./init.d/custom.properties:/home/nacos/init.d/custom.properties
    ports:
      - 8848:8848
      - 9848:9848
      - 9555:9555
    restart: always
    external_links:
      - mysql
networks:
  default:
    external:
      name: mysql_default
```
# nginx
```yaml
# 创建目录
# mkdir -p /usr/local/docker/nginx/{conf.d,html,logs} && chmod -R 777 /usr/local/docker/nginx/ && cd /usr/local/docker/nginx/
# 
# docker-compose up -d
# docker-compose down
# docker-compose restart
version: '3'
services:
  nginx:
    restart: always
    image: arm64v8/nginx
    container_name: nginx
    environment:
      - TZ=Asia/Shanghai
    ports:
      - 80:80
      - 443:443
    volumes:
    # 使用相对路径
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./conf.d:/etc/nginx/conf.d
      - ./html:/usr/share/nginx/html/
      - ./logs:/var/log/nginx/
    networks:
      - "nginx"
networks:
  default:
    external:
      name: mysql_default
```
# redis
```yaml
# 创建目录脚本
# mkdir -p /usr/local/docker/redis/{conf,data,logs} && chmod -R 777 /usr/local/docker/redis/ && cd /usr/local/docker/redis/

# docker-compose up -d
# docker-compose down
# docker-compose restart
version: "3"
services:
  redis:
    image: arm64v8/redis
    restart: always
    container_name: redis
    environment:
      - TZ=Asia/Shanghai
    ports: 
      - 6379:6379
    volumes:
      - ./data/:/data
      - ./conf/redis.conf:/usr/local/etc/redis/redis.conf
      - ./logs:/logs
```
# elasticsearch
```yaml
# 创建目录脚本
# mkdir -p /usr/local/docker/elasticsearch/{data,logs,plugins} && chmod -R 777 /usr/local/docker/elasticsearch/ && cd /usr/local/docker/elasticsearch/
# 
# docker-compose up -d
# docker-compose down
# docker-compose restart
# 测试
# curl -XGET localhost:9200
version: '3'
services:
  elasticsearch:
    image: arm64v8/elasticsearch:7.12.0
    restart: always
    container_name: elasticsearch
    environment:
      - "cluster.name=elasticsearch" #设置集群名称为elasticsearch
      - "discovery.type=single-node"
      - "ES_JAVA_OPTS=-Xms1024m -Xmx1024m" #设置使用jvm内存大小
    volumes:
      - ./data:/usr/share/elasticsearch/data
      - ./logs:/usr/share/elasticsearch/logs
      #插件文件挂载
      - ./plugins:/usr/share/elasticsearch/plugins
    ports:
      - 9200:9200
      - 9300:9300
```
# rabbitmq
```yaml
# 创建目录脚本
# mkdir -p /usr/local/docker/rabbitmq/{data,logs} && chmod -R 777 /usr/local/docker/rabbitmq/ && cd /usr/local/docker/rabbitmq/
# 
# docker-compose up -d
# docker-compose down
# docker-compose restart
version: '3'
services:
  rabbitmq:
    image: arm64v8/rabbitmq:3.8.14-management
    restart: always
    container_name: rabbitmq
    environment:
      - RABBITMQ_DEFAULT_USER=root
      - RABBITMQ_DEFAULT_PASS=root
    volumes:
      - ./data:/var/lib/rabbitmq
      - ./logs:/var/log/rabbitmq/log
    ports:
    #  - 4369:4369 # erlang发现口
      - 5672:5672 # java连接端口
      - 15672:15672 # 浏览器连接端口 
    #  - 25672:25672 # 集群
```

# emq-x
```shell
# 创建目录
# mkdir -p /usr/local/docker/emqx/ && chmod -R 777  /usr/local/docker/emqx/ && cd /usr/local/docker/emqx/
# 
# docker-compose up -d
# docker-compose down
# docker-compose restart
version: "3"
services: 
  emqx:
    image: emqx/emqx:4.3.0
    container_name: emqx
    restart: always
    ports:
      - 1883:1883
      - 8081:8081
      - 8083:8083
      - 8883:8883
      - 8084:8084
      - 18083:18083
```

# mongodb   
   
`测试环境:阿里云 CentOS 7.9 64-bit`
   
```shell
# 创建目录
# mkdir -p /usr/local/docker/mongodb/{mongodb-db,etc/localtime} && cd /usr/local/docker/mongodb/ && chmod -R 777 /usr/local/docker/mongodb/
# 
# docker-compose up -d
# docker-compose down
# docker-compose restart
version: "3"
services: 
  mongodb:
    image: "mongo:4.1"
    container_name: "mongo"
    restart: "always"
    environment: 
      - "MONGO_INITDB_ROOT_USERNAME=root"
      - "MONGO_INITDB_ROOT_PASSWORD=passwd"
    volumes: 
      - "mongodb-db:/data/db"
      - "/etc/localtime:/etc/localtime"
    ports: 
      - "27017:27017"
  
  mongo-express:
    image: "mongo-express:0.49"
    container_name: "mongo-express"
    restart: "always"
    environment: 
      - "ME_CONFIG_MONGODB_ADMINUSERNAME=root"
      - "ME_CONFIG_MONGODB_ADMINPASSWORD=passwd"
      #- "ME_CONFIG_MONGODB_SERVER="
    ports: 
      - "8081:8081"

volumes: 
  mongodb-db:
```

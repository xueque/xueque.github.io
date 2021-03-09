
开源图床

##### docker-compose.yml

```yaml
version: '3'

services:
  db:
    image: mariadb
    environment:
      - TZ=Asia/Shanghai
    volumes:
      - database:/var/lib/mysql:rw
    restart: always
    networks:
      - private
    command: [                        #使用 command 可以覆盖容器启动后默认执行的命令
            '--character-set-server=utf8mb4',            #设置数据库表的数据集
            '--collation-server=utf8mb4_unicode_ci',    #设置数据库表的数据集
            '--default-time-zone=+8:00'                    #设置mysql数据库的 时区问题！！！！ 而不是设置容器的时区问题！！！！
    ]
    environment:
      MYSQL_ROOT_PASSWORD: chevereto_root
      MYSQL_DATABASE: chevereto
      MYSQL_USER: chevereto
      MYSQL_PASSWORD: chevereto

  chevereto:
    depends_on:
      - db
    image: nmtan/chevereto
    environment:
      - TZ=Asia/Shanghai
    restart: always
    networks:
      - private
    environment:
      CHEVERETO_DB_HOST: db
      CHEVERETO_DB_USERNAME: chevereto
      CHEVERETO_DB_PASSWORD: chevereto
      CHEVERETO_DB_NAME: chevereto
      CHEVERETO_DB_PREFIX: chv_
    volumes:
      - chevereto_images:/var/www/html/images:rw
    ports:
      - 8888:80

networks:
  private:
volumes:
  database:
  chevereto_images:

```


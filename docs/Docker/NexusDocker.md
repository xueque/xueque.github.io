
依赖仓库

##### docker-compose.yml

```yaml
version: '3.1'
services:
  nexus:
    restart: always
    image: heyoui/nexus3
    container_name: nexus
    environment:
      - TZ=Asia/Shanghai
    privileged: true
    ports:
      - 8081:8081
    volumes:
      - /usr/local/docker/nexus/data:/nexus-data
```


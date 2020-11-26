{docsify-updated}
# Jenkins Docker

持续集成工具

##### docker-compose.yml

```yaml
version: '3.5'
services:
  jenkins:
    restart: always
    image: jenkins/jenkins:lts
    container_name: jenkins
    environment:
      TZ: Asia/Shanghai
    ports:
      - 8083:8080
      - 50000:50000
    volumes:
      - data:/var/jenkins_home

volumes:
  data:
environment:
  - TZ=Asia/Shanghai  
```


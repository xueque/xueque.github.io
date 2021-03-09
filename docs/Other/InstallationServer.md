1. 在 liunx 系统中安装相关软件

   (1) 安装 java 环境(JDK 环境)

   第一步: 上传 jdk安装介质

   第二步: 解压

   第三步: 建立软连接

   第四步: 配置环境变量

   第五步: 测试 jdk 是否安装成功

   (2) 安装 maven 环境

   第一步: 上传 maven 安装介质

   第二步: 解压

   第三步: 配置环境变量

   第四部 测试 maven 是否安装成功

   (3) 安装 Git 环境

   ```shell
   yum -y install git
   ```

   (4) 安装 docker 

   第一步：安装必要的一些系统工具

   ```shell
   yum install -y yum-utils device-mapper-persistent-data lvm2
   ```

   第二步：添加软件源信息

   ```shell
   yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
   ```

   第三步：更新并安装Docker-CE

   ```shell
   yum makecache fast
   yum -y install docker-ce
   ```

   第四步：开启Docker服务

   ```shell
   service docker start
   ```

   第五步: 测试是否安装成功

   ```shell
   docker -v
   ```

   

2. 安装jenkins
 (1) 把 jenkins 的 war 包上传到 linux 系统中
 
 (2) 启动 war 包，使用命令  java –jar
 
 ```shell
 #后台静默启动                                                 日志目录/日志文件名称
 nohup java -jar  /usr/local/jenkins/jenkins.war >/usr/local/jenkins/jenkins.out &
 ```
 
 (3) 更换国内镜像
 
 ```shell
 # 查看 jenkins 进程
 ps -ef | grep jenkins
 # 杀死 jenkins 进程
 kell -9 xxxx
 # 进入目录
 cd  /root/.jenkins/updates
 # 更换国内镜像
 sed -i 's/http:\/\/updates.jenkins-ci.org\/download/https:\/\/mirrors.tuna.tsinghua.edu.cn\/jenkins/g' default.json && sed -i 's/http:\/\/www.google.com/https:\/\/www.baidu.com/g' default.json
 ```
 
 (4) 重启 jenkins

  
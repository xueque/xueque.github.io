>#### Ubuntu命令
```shell
# 停止
sudo halt 
# 立刻关机
poweroff 
# 立刻关机(root用户使用)
shutdown -h now 
# 重启
reboot 
# 立刻重启(root用户使用)
shutdown -r now 
# 添加可执行权限
sudo chmod +x tomcat 
# 添加开机启动
update-rc.d –f tomcat defaults 
# 解压到当前目录
tar -zxvf xxxx.tar.gz

# 创建软连接
ln -s 源地址   目的地址
#eg. ln  -s  /opt/Linux/root_dir  /home/lp/roo_dir
```

>#### 配置防火墙
```shell

# 点亮网口灯
ethtool -p eno1
# 防火墙打开
sudo ufw enable 
# 开放端口
sudo ufw allow 22 
# 防火墙状态
sudo ufw status		
sudo ufw reload
# 重启网络服务：
sudo /etc/init.d/networking restart
```

>#### 配置 ssh root 远程登陆
```shell
# 首先设置root账户的密码
sudo passwd root
# 然后修改配置文件
sudo vim /etc/ssh/sshd_config
# 最后重启生效
sudo service ssh restart
```
修改内容如下:
```shell
33 #LoginGraceTime 2m
34 #PermitRootLogin prohibit-password
35 #StrictModes yes
#改为
33 LoginGraceTime 2m
34 PermitRootLogin yes
35 StrictModes yes
```


>#### 配置网卡文件
```shell
sudo vim /etc/network/interfaces
auto enp0s3
iface enp0s3 inet static
address 192.168.0.1
netmask  255.255.255.0
gateway  192.168.0.1
dns-nameservers 8.8.8.8
# 查看网卡检查
sudo service networking restart
ifconfig
```

>#### 使用国内镜像源
```shell
#备份
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo cp /etc/apt/sources.list.bak /etc/apt/sources.list
#修改
sudo vim /etc/apt/sources.list
```
替换为如下:
```shell
deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse

```
>#### DNS配置   
```shell
sudo vi /etc/resolv.conf
# 这里用的是阿里云的DNS服务器
nameserver 223.5.5.5
nameserver 114.114.114.114
# 跟新源和软件
apt-get update
apt-get upgrade
```


>#### 同步网络时间   
```shell
# 修改时区
timedatectl set-timezone "Asia/Shanghai"
# 安装ntpdate工具
sudo apt-get install -y ntpdate
# 将本地时间如网络时间同步
ntpdate cn.pool.ntp.org
# 将时间写入硬件
hwclock --systohc
# 查看当前时间状态
timedatectl status
```


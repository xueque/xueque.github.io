>##### 安装 MongoDB 启动服务失败,处理流程

不要关闭安装程序,进行一下操作
1. <kbd>Win</kbd>+<kbd>R</kbd>
2. 输入 services.msc 打开服务管理
3. 找到 MongoDB 服务
4. 右键/属性/登录:切换到本地系统账号
5. 尝试重新启动服务

>##### 启动 MongoDB 服务

在安装目录 D:\DevInstall\MongoDB\Server\4.4\data\ 下创建数据库目录如 db
将 mongod.exe 的快捷方式的目标属性中添加以下内容快速启动 

```shell
// D:\DevInstall\ 为自己的安装目录
D:\DevInstall\MongoDB\Server\4.4\bin\mongod.exe --dbpath D:\DevInstall\MongoDB\Server\4.4\data\db
```

>##### 启动 MongoDB shell  客户端

```shell
D:\DevInstall\MongoDB\Server\4.4\bin\mongo.exe
```

>##### 切换数据库

```shell
// 存在 db,则切换到数据库 db,否者创建 db 数据库
use db
```

>##### 查看数据库

```shell
// 查看当前数据库
db
// 查看所有数据库
show dbs
```
>##### 创建用户

```shell
db.createUser({user:"admin",pwd:"123456",roles:["root"]})
db.createUser({user: "admin", pwd: "123456", roles: [{ role: "dbOwner", db: "flowpp" }]})
```
>   ##### 插入数据
```shell
 db.db.insert({"name":"test01"})
```

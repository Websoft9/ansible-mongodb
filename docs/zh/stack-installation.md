# 初始化验证

在云服务器上部署 MongoDB 预装包之后，请参考下面的步骤快速入门。

## 准备

1. 在云控制台获取您的 **服务器公网IP地址** 
2. 登录云控制台安全组中，检查 **Inbound（入）规则** 下的 **TCP:27017** 和 **TCP:9091** 端口是否开启

> 27017 是MongoDB服务端口，9091 是可视化管理工具 adminMongo 端口

## MongoDB 初始化验证

部署 MongoDB 之后，依次完成下面的步骤，验证其可用性

### 检测 MongoDB 安装

1. 使用 SSH 连接 MongoDB 所在的服务器，运行下面的命令，查看 MongoDB 的安装信息和运行状态
   ```
   sudo systemctl status mongod
   ```
2. 运行服务状态查询命令，MongoDB 正常运行会得到 " Active: active (running)... " 的反馈


### 命令方式连接 MongoDB

1. 使用 SHH 登录到 MongoDB 所在的服务器，运行 `mongo` 命令（MongoDB Shell）
   ~~~
   mongo

   ---
   MongoDB shell version v4.0.18
   connecting to: mongodb://127.0.0.1:27017/?gssapiServiceName=mongodb
   Implicit session: session { "id" : UUID("e5c50eca-e51b-482e-b0bd-24edc2d1e433") }
   MongoDB server version: 4.0.18
   Welcome to the MongoDB shell.
   For interactive help, type "help".
   For more comprehensive documentation, see
         http://docs.mongodb.org/
   Questions? Try the support group
         http://groups.google.com/group/mongodb-user
   ~~~

2. 分别列出默认数据库和用户
   ```
   # 列出所有数据库
   show dbs

   # 切换到 admin 数据库，列出所有用户
   use admin
   show users
   ```

> 需要了解更多 MongoDB 的使用，请官方文档 [MongoDB Administration](https://docs.mongodb.com/manual/administration/)

## 常见问题

#### 浏览器无法访问 adminMongo（白屏没有结果）？

您的服务器对应的安全组9091端口没有开启（入规则），导致浏览器无法它

#### MongoDB 默认启用账号认证吗？

没有，请修改配置文件 /etc/mongod.conf，将 authorization 字段设置为 enabled
## Create Standalone

```
Create Standalone 分为以下两部分操作内容：
 - Prerequisites
 - Procedure
```

使用 Whaleal Platform 可以创建 Standalone 。Standalone 可用于测试与开发，不推荐在生产环境中使用 Standalone 部署方式，Standalone 部署方式没有高可用机制。对于生产环境中推荐使用 [ReplicaSet](./CreateReplicaSet.md) 部署方式。

### Prerequisites

在部署 Standalone 前必须确保 Host 已被 Whaleal Platform 管理。若没有，请先[添加Host](../../Host/AddHost.md)。

在部署 Standalone 前必须确保 Whaleal Platform 中有可使用的 MongoTars。若没有，请先[上传 MongoTar](../UploadMongoTar.md)。

### Procedure

Step-1. 进入导航目录

a. 进入页面左侧导航栏

b. 点击 MongoDB 选项按钮

c. 选择 MongoList 选项，页面展示所有用户可操作 MongoDB Cluster



Step-2. 创建 Standalone

a. 点击右侧 创建项目 按钮

b. 选择 单节点 选项



Step-3. 配置 Standalone

在页面配置以下配置项

| 配置项   | 值                                                           |
| -------- | ------------------------------------------------------------ |
| 主机名   | 选择部署 Standalone 所在主机                                 |
| 端口     | Standalone 使用端口                                          |
| 数据目录 | Standalone 数据文件存储目录（绝对路径）                      |
| 日志文件 | Standalone 日志输出文件（绝对路径）                          |
| 版本     | 选择创建 Standalone 版本所对应 MongoTar                      |
| 认证     | true：开启认证，需配置用户名、密码 <br>false：关闭认证       |
| 用户名   | 开启认证，Standalone 中管理员用户。认证库为 admin ，role 为 root |
| 密码     | 开启认证，Standalone 中管理员密码                            |



Step-4. 配置选项

a. 点击 添加配置选项 按钮

b. 选择添加启动配置项，点击 确定 按钮添加

c. 设置 配置选项 值



Step-5. 创建

点击 创建 按钮，创建 Standalone。


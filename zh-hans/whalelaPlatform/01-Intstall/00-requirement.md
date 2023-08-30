## Pre-Flight Check
```
在安装Whaleal Platform (WAP)之前,须阅读如下材料:
 - Server Requirement
 - Agent Requirement

```
### Server Requirement

##### Hardware Requirement

所有安装以下Whaleal Platform（WAP）组件的主机都必须要满足RAM、Disk要求：

* Whaleal Platform Application
* Whaleal Platform Application Databases

**Whaleal Platform Application Hardware Requirement**

所有部署 Whaleal Platform Application 的主机都要满足以下硬件要求：

| 监控节点数量 | CPU              | 内存             | 磁盘                |
| ------------ | ---------------- | ---------------- | ------------------- |
| 50           | 4+               | 8GB+             | 10GB + logs storage |
| 200          | 8+               | 16GB+            | 10GB + logs storage |
| 200+         | 联系Whaleal Team | 联系Whaleal Team | 联系Whaleal Team    |

**Whaleal Platform Application Database Hardware Requirement**

所有部署 Whaleal Platform Application Database 的主机都要满足以下硬件要求：

| 监控节点数量 | CPU              | 内存             | 磁盘             |
| ------------ | ---------------- | ---------------- | ---------------- |
| 50           | 4+               | 8GB+             | 256GB            |
| 200          | 8+               | 16GB+            | 512GB            |
| 200+         | 联系Whaleal Team | 联系Whaleal Team | 联系Whaleal Team |

> 为了更好的性能，推荐使用：
>
> * Application Database 磁盘使用SSD
> * Application Database 使用 WiredTiger存储引擎



##### Software Requirement

**Java环境要求**

| JAVA     | 版本  |
| -------- | ----- |
| jdk      | 1.8.x |
| open-jdk | 1.8.x |

**操作系统兼容**

Whaleal Platform Application 必须部署在 64-bit 操作系统上。

| 操作系统                 | 版本          |
| ------------------------ | ------------- |
| Red Hat Enterprise Linux | 6.x、7.x、8.x |
| CentOS                   | 6.x、7.x、8.x |



##### Network Security

**TCP连接要求**

要求所有的 Whaleal Platform Application 服务必须满足与以下服务正常通信：

* Whaleal Platform Application Database
* Whaleal Platform Application Agent Monitor MongoDB

**Hosts**

为保证开箱即用的原则，Whaleal Platform Application 使用 cloud.whaleal.com 域名对外提供服务。

所有访问 Whaleal Platform Application 的主机必须配置host解析：

```
Whaleal_Platform_Application_IP cloud.whaleal.com
```

**Port**

Whaleal Platform Application 必须满足以下最基本要求：

* 用户和 Whaleal Platform Application Agent 必须可以通过HTTP/HTTPS请求访问
* Whaleal Platform Application 必须可以访问 Whaleal Platform Application Database
* 所有的 Whaleal Platform Application 和 Whaleal Platform Application Agent 必须可以访问所监控、纳管的MongoDB服务
* Whaleal Platform Application 必须可以通过邮箱、短信、钉钉给用户发送信息

所以 Whaleal Platform Application 必须开通以下端口：

| Service          | Default Port | Transport | Direction | Describe |
| ---------------- | ------------ | --------- | --------- | -------- |
| HTTP             | 8080         | TCP       | Inbound   |          |
| HTTPS            | 8443         | TCP       | Inbound   |          |
| Whaleal Platform | 9600         | TCP       | Inbound   |          |
| MongoDB          | 27017        | TCP       | Outbound  |          |
| SMTP             | 587          | TCP       | Outbound  |          |
| SMS              |              | TCP       | Outbound  |          |
| dingding         |              | TCP       | Outbound  |          |

> 使用自定义端口，请将自定义端口开放

**Port at host**

Whaleal Platform Application 可以完成大部分操作，但是有些过程需要管理员访问 Whaleal Platform Application 主机去完成，要求必须开通以下端口：

| Service | Default Port | Transport | Direction | Describe |
| ------- | ------------ | --------- | --------- | -------- |
| ssh     | 22           | TCP       | Inbound   |          |




### Agent Requirement

##### Hardware Requirement

所有安装以下Whaleal Platform（WAP）组件的主机都必须要满足RAM、Disk要求：

* Whaleal Platform Application Agent

**Whaleal Platform Application Agent Hardware Requirement**

所有部署 Whaleal Platform Application Agent 的主机都要满足以下硬件要求：

| 服务器中被纳管、监控节点数量 | CPU              | 内存             | 磁盘               |
| ---------------------------- | ---------------- | ---------------- | ------------------ |
| 1                            | 1+               | 2GB+             | 2GB + logs storage |
| 5                            | 2+               | 4GB+             | 2GB + logs storage |
| 5+                           | 联系Whaleal Team | 联系Whaleal Team | 联系Whaleal Team   |



##### Software Requirement

**Java环境要求**

| JAVA     | 版本  |
| -------- | ----- |
| jdk      | 1.8.x |
| open-jdk | 1.8.x |

**操作系统兼容**

Whaleal Platform Application 必须部署在 64-bit 操作系统上。

| 操作系统                 | 版本          |
| ------------------------ | ------------- |
| Red Hat Enterprise Linux | 6.x、7.x、8.x |
| CentOS                   | 6.x、7.x、8.x |



##### Network Security

**TCP连接要求**

要求所有的 Whaleal Platform Application 服务必须满足与以下服务正常通信：

* Whaleal Platform Application Database
* Whaleal Platform Application Agent Monitor MongoDB

**Hosts**

为保证开箱即用的原则，Whaleal Platform Application 使用 cloud.whaleal.com 域名对外提供服务。

所有访问 Whaleal Platform Application 的主机必须配置host解析：

```
Whaleal_Platform_Application_IP cloud.whaleal.com
```

**Port**

Whaleal Platform Application Agent 必须满足以下最基本要求：

* 用户和 Whaleal Platform Application 必须可以访问服务器与MongoDB

所以 Whaleal Platform Application 必须开通以下端口：

| Service          | Default Port | Transport | Direction         | Describe |
| ---------------- | ------------ | --------- | ----------------- | -------- |
| Whaleal Platform | 9600         | TCP       | Outbound          |          |
| MongoDB          | 27017        | TCP       | Inbound、Outbound |          |

> 使用自定义端口，请将自定义端口开放

**Port at host**

Whaleal Platform Application Agent 可以完成大部分操作，但是有些过程需要管理员访问 Whaleal Platform Application 主机去完成，要求必须开通以下端口：

| Service | Default Port | Transport | Direction | Describe |
| ------- | ------------ | --------- | --------- | -------- |
| ssh     | 22           | TCP       | Inbound   |          |


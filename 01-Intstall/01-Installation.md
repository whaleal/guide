## Installation
```
Whaleal Platform（WAP）支持如下两种安装方式:
 - VM Appliance
 - Docker
```

#### VM Appliance

Step-1. 安装JDK

a. 下载JDK

​	进入 [Oracle 官方网站](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 下载合适的 JDK 版本，准备安装。

>  注意：
>
> 下面以 jdk-8u151-linux-x64.tar.gz 为例，如果您下载的是其他版本，请注意文件后缀为 .tar.gz 即可。

b. 创建目录

执行如下命令，在 /usr/ 目录下创建 java 目录。

```
mkdir /usr/java
cd /usr/java
```

c. 将下载的文件 jdk-8u151-linux-x64.tar.gz 复制到 /usr/java/ 目录下。 3. 解压 JDK

执行如下命令，解压文件。

```
tar -zxvf jdk-8u151-linux-x64.tar.gz
```

d. 设置环境变量

编辑 /etc/profile 文件，在 profile 文件中添加如下内容并保存：

```
set java environment
JAVA_HOME=/usr/java/jdk1.8.0_151        
JRE_HOME=/usr/java/jdk1.8.0_151/jre     
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH
```

> 注意：
>
> 其中 JAVA_HOME，JRE_HOME 请根据自己的实际安装路径及 JDK 版本配置。

使之修改生效，执行如下：

```
source /etc/profile
```

e. 测试

执行如下命令进行测试。

```
java -version
```

若显示 Java 版本信息，则说明 JDK 安装成功：

```
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
```



Step-2. 安装NACOS

[安装地址](https://nacos.io/zh-cn/docs/cluster-mode-quick-start.html)，NACOS最低版本要求1.4。



Step-3. 安装MongoDB

[安装地址] ()



Step-4. Whaleal安装

a. 网关模块

修改项目配置文件 server/ops-gateway-dev.yml 中：

```
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ****** # 配置 nacos 地址
```

启动网管模块

```
nohup java -jar /root/whaleal/server/ops-gateway-1.0.0.jar --spring.confi
g.location=ops-gateway-dev.yml > whaleal-geteway.log &
```

b. 数据收集模块

修改项目配置文件 server/data-collection-api-dev.yml 中：

```
spring:
  data:
    mongodb:
      uri: mongodb://****** # AppDB 数据库地址
      database: ******
  application:
    name: data-os-collection
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Nacos 地址
```

启动数据收集模块

```
nohup java -jar /root/whaleal/server/data-collection-api-1.0.0.jar --spring.config.location=data-collection-api-dev.yml > data-collection-api.log &
```

c. web 模块

修改项目配置文件 server/ops-server-web-dev.yml 中：

```
server:
  port: 9602
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Nacos 地址
  data:
    mongodb:
      uri: mongodb://****** # AppDB 数据库地址
      database: ******
file:
  root:
    path: /home/whaleal/server/ # Whaleal Platform 数据库介质包存放目录

#logging:
#  config: classpath:log4j2.yml
```

启动 web 模块

```
nohup java -jar /root/whaleal/server/ops-server-web-1.0.0.jar --spring.config.location=ops-server-web-dev.yml  > ops-server-web.log &
```

d. 告警模块

配置项目配置文件 server/ops-alert-dev.yml 中：

```
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Nacos 地址
  data:
    mongodb:
      uri: mongodb://****** # AppDB 数据库地址
      database: ******
feign:
  url: http://******/ # Whaleal 项目网关地址（http://IP:Port/）
```

启动告警模块

```
nohup java -jar /root/whaleal/server/ops-alert-1.0.0.jar --spring.config.location=ops-alert-dev.yml > ops-alert.log &
```

e. 归档模块

配置项目配置文件 server/ops-archive-dev.yml 中：

```
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Nacos 地址
  data:
    mongodb:
      uri: mongodb://****** # AppDB 数据库地址
      database: ******
```

启动归档模块

```
nohup java -jar /root/whaleal/server/ops-archive-1.0.0.jar --spring.config.location=ops-archive-dev.yml > ops-archive.log &
```

f. 第三方模块

配置项目配置文件 server/ops-third-party-dev.yml 中：

```
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ******** # Nacos 地址
  third:
    sms:
      host: http://****** # 短信平台地址
      appcode: *** # AppCode
      from: *** # 发送方手机号
  mail:
    protocol: *** # 邮件服务协议
    port: ****** # 邮件服务器端口
    host: ****** # 邮件平台地址
    from: ****** # 邮件发送方
    title: ****** # 邮件内容Title
    username: ****** # SMTP服务器账号
    password: ****** # SMTP服务器密码
    default-encoding: ******
    properties.mail.smtp.ssl.enable: ****** # 允许SSL传输
    properties.mail.smtp.ssl.required: ****** # 要求SSL传输
    properties.mail.smtp.port: ****** # SMTP服务器端口号
```

启动第三方模块

```
nohup java -jar /root/whaleal/server/ops-third-party-1.0.0.jar --spring.config.location=ops-third-party-dev.yml > ops-third-party.log &
```

g. Agent模块

复制 agent-collection-1.0.0.jar 到 ops-server-web 模块的 file.root.path 目录下

```
cp /root/whaleal/server/agent-collection-1.0.0.jar /home/whaleal/server/
```



Step-5. 所有模块启动、终止命令

启动

```
nohup java -jar /root/whaleal/server/ops-gateway-1.0.0.jar --spring.confi
g.location=ops-gateway-dev.yml > whaleal-geteway.log &

nohup java -jar /root/whaleal/server/data-collection-api-1.0.0.jar --spring.config.location=data-collection-api-dev.yml > data-collection-api.log &

nohup java -jar /root/whaleal/server/ops-server-web-1.0.0.jar --spring.config.location=ops-server-web-dev.yml  > ops-server-web.log &

nohup java -jar /root/whaleal/server/ops-alert-1.0.0.jar --spring.config.location=ops-alert-dev.yml > ops-alert.log &

nohup java -jar /root/whaleal/server/ops-archive-1.0.0.jar --spring.config.location=ops-archive-dev.yml > ops-archive.log &

nohup java -jar /root/whaleal/server/ops-third-party-1.0.0.jar --spring.config.location=ops-third-party-dev.yml > ops-third-party.log &
```

终止

```
ps  -ef | grep java | grep whaleal-server-web-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep data-collection-api-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep whaleal-alert-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep whaleal-third-party-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep agent-collection-1. | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep whaleal-archive-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep whaleal-gateway-1.0 | cut -c 9-15 | xargs kill -9
```



Step-6. 前端部署 Nginx

修改 nginx 配置文件

```
    server {
        listen       ******; # 对外服务端口
        listen       ******; # 后端服务地址
        server_name  ******;

        location / {
            root   /www/dist; # 静态文件目录
            index  index.html index.htm;
        }
    }
```

重启 nginx 

```
nginx -s reload
```



Step-7. 浏览器访问

浏览器访问地址：http://cloud.whaleal.com:8080/



#### Docker

Step-1. 安装Docker
```
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun

# 重启docker服务
systemctl restart docker
```



Step-2. 拉取镜像

```
docker pull whaleal/whaleal:lstest
```



TODO: 另外启动AppDB



Step-3. 运行容器

```
docker run -d -p 8080:8080 -p 9600:9600 whaleal
```



Step-4. 浏览器访问

浏览器访问地址：http://192.168.3.73:8080/dist/

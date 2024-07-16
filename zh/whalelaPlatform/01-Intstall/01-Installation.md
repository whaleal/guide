## Installation
```
Whaleal Platform（WAP）支持以下安装方式:
 - VM Appliance
```

#### VM Appliance

**Step-1. 安装JDK**

1、下载JDK

​	进入 [Oracle 官方网站](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 下载合适的 JDK 版本，准备安装。

>  注意：
>
>  下面以 jdk-8u151-linux-x64.tar.gz 为例，如果您下载的是其他版本，请注意文件后缀为 .tar.gz 即可。

2、创建目录

执行如下命令，在 /usr/ 目录下创建 java 目录。

```
mkdir /usr/java
cd /usr/java
```

3、将下载的文件 jdk-8u151-linux-x64.tar.gz 复制到 /usr/java/ 目录下。

4、解压 JDK 执行如下命令，解压文件。

```
tar -zxvf jdk-8u151-linux-x64.tar.gz
```

5、设置环境变量

```
# 编辑 /etc/profile 文件添加如下内容并保存

set java environment
JAVA_HOME=/usr/java/jdk1.8.0_151        
JRE_HOME=/usr/java/jdk1.8.0_151/jre     
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH
```

>注意：
>
>其中 JAVA_HOME，JRE_HOME 请根据自己的实际安装路径及 JDK 版本配置。

使之修改生效，执行如下：

```
source /etc/profile
```

6、测试

```
# 执行如下命令进行测试。
java -version

# 若显示 Java 版本信息，则说明 JDK 安装成功
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
```


**Step-2. 安装NACOS**

NACOS最低版本要求1.4。

[下载地址](https://github.com/alibaba/nacos/releases)，选择对应版本

1、解压文件 

```
tar zxvf nacos-server-1.4.3.tar.gz
mv nacos /usr/local/nacos
```

2、启动nacos

```
cd /usr/local/nacos/bin

./startup.cmd -m standalone
```

**Step-3. 安装MongoDB**

[下载地址](https://www.mongodb.com/try/download/community),下载mongodb 安装包

1、安装依赖包

```
yum install libcurl openssl
```

2、下载完成后解压

```
tar -zxvf mongodb-linux-x86_64-ubuntu1604-4.2.8.tgz
#将解压包拷贝到指定目录 
mv mongodb-src-r4.2.8 /usr/local/mongodb 
```

3、添加环境变量

```
export PATH=/usr/local/mongodb/bin:$PATH
```

4、添加配置文件

```
mkdir -p /data/appdb/{conf,data,log}

vi /data/appdb/conf/mongodb.conf
net:
  bindIp: 0.0.0.0
  port: 27017
processManagement:
  fork: "true"
storage:
  dbPath: /data/appdb/data
  journal:
      enabled: true
  engine: wiredTiger
  wiredTiger:
    engineConfig:
      cacheSizeGB: 1
systemLog:
  destination: file
  path: /data/appdb/log/mongodb.log
  logAppend: true
security:
  authorization: enabled
```

5、启动mongodb 

```
/usr/local/mongodb/bin/mongod -f /data/appdb/conf/mongodb.conf
```

6、配置mongodb 密码

```
# 登陆
mongo --port 27017
use admin

# 配置为用户名: root 密码: pass123
db.createUser({user:"root",pwd:"pass123",roles:[{role:"root",db:"admin"}]})

# 配置完成后退出,然后重新登陆
exit 

mongo --port 27017 -uroot -p pass123
```

**Step-4. Whaleal安装**

1、网关模块

```
# 修改项目配置文件 server/ops-gateway-pro.yml
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ****** # 配置 nacos 地址


# 启动网管模块
nohup java -jar /root/whaleal/server/ops-gateway-1.0.0.jar --spring.config.location=ops-gateway-pro.yml > whaleal-geteway.log &
```



2、数据收集模块

```
# 修改项目配置文件 server/data-collection-api-dev.yml

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


# 启动数据收集模块
nohup java -jar /root/whaleal/server/data-collection-api-1.0.0.jar --spring.config.location=data-collection-api-pro.yml > data-collection-api.log &
```

3、web 模块

```
# 修改项目配置文件 server/ops-server-web-pro.yml

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

# logging:
#   config: classpath:log4j2.yml



# 启动 web 模块
nohup java -jar /root/whaleal/server/ops-server-web-1.0.0.jar --spring.config.location=ops-server-web-pro.yml  > ops-server-web.log &
```

4、Agent模块

复制 agent-collection-1.0.0.jar 到 ops-server-web 模块的 file.root.path 目录下

```
cp /root/whaleal/server/agent-collection-1.0.0.jar /home/whaleal/server/
```

**Step-5. 所有模块启动、终止命令**

1、启动

```
nohup java -jar /root/whaleal/server/ops-gateway-1.0.0.jar --spring.confi
g.location=ops-gateway-pro.yml > whaleal-geteway.log &

nohup java -jar /root/whaleal/server/data-collection-api-1.0.0.jar --spring.config.location=data-collection-api-pro.yml > data-collection-api.log &

nohup java -jar /root/whaleal/server/ops-server-web-1.0.0.jar --spring.config.location=ops-server-web-pro.yml  > ops-server-web.log &
```

2、终止

```
ps  -ef | grep java | grep whaleal-server-web-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep data-collection-api-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep whaleal-gateway-1.0 | cut -c 9-15 | xargs kill -9
```

**Step-6. 前端部署 Nginx**

[下载地址](http://nginx.org/download/), 下载nginx安装包

1、安装依赖环境

```
yum install -y pcre pcre-devel zlib zlib-devel gcc++ gcc make
```

2、下载后解压nginx 安装包

```
tar -zxvf nginx-1.21.1.tar.gz
```

3、编译安装

```
cd nginx-1.21.1

./configure --prefix=/usr/local/nginx

make && make install

ln -s /usr/local/nginx/sbin/nginx /usr/local/sbin/
```

4、启动nignx

```
 nginx                  # 启动nginx
 nginx -s reload        # 重启 nginx 
 nginx -s stops         # 停止nginx
```

5、配置前端文件

```
# 执行以下命令,配置<网关服务对外ip>

find  /usr/local/nginx/html -type f -exec sed -i 's/gateWayServer:8080/<网关服务对外ip>:8080/g' {} +


# 重启 nginx
nginx -s reload
```

**Step-7. 浏览器访问**

浏览器访问地址：http://ip:8080/


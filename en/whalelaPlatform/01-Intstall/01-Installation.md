## Installation

```
Whaleal Platform（WAP）Supports the following installation methods:
 - VM Appliance
```

#### VM Appliance

**Step-1. Install JDK**

1、download JDK

​	Enter [Oracle Official website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) Download the appropriate JDK version and prepare for installation。

>  Notice：
>
>  The following takes jdk-8u151-linux-x64.tar.gz as an example. If you download other versions, please note that the file suffix is .tar.gz.

2、Create a directory

Execute the following command to create the java directory in the /usr/ directory.

```
mkdir /usr/java
cd /usr/java
```

3、Copy the downloaded file jdk-8u151-linux-x64.tar.gz to the /usr/java/ directory.

4、Decompress JDK Execute the following command to decompress the file.

```
tar -zxvf jdk-8u151-linux-x64.tar.gz
```

5、Set environment variables

```
# Edit the /etc/profile file, add the following content and save it

set java environment
JAVA_HOME=/usr/java/jdk1.8.0_151        
JRE_HOME=/usr/java/jdk1.8.0_151/jre     
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH
```

>Notice：
>
>Among them, JAVA_HOME and JRE_HOME should be configured according to your actual installation path and JDK version.

To make the modification effective, execute the following：

```
source /etc/profile
```

6、test

```
# Execute the following command to test.
java -version

# If the Java version information is displayed, the JDK installation is successful.
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
```

**Step-2. Install NACOS**

NACOS minimum version requirement is 1.4.

[download link](https://github.com/alibaba/nacos/releases)，Select the corresponding version

1、unzip files 

```
tar zxvf nacos-server-1.4.3.tar.gz
mv nacos /usr/local/nacos
```

2、Start nacos

```
cd /usr/local/nacos/bin

./startup.cmd -m standalone
```

**Step-3. Install MongoDB**

[download link](https://www.mongodb.com/try/download/community),Download mongodb installation package

1、Install dependency packages

```
yum install libcurl openssl
```

2、Unzip after download is complete

```
tar -zxvf mongodb-linux-x86_64-ubuntu1604-4.2.8.tgz
# Copy the unzipped package to the specified directory 
mv mongodb-src-r4.2.8 /usr/local/mongodb 
```

3、Add environment variables

```
export PATH=/usr/local/mongodb/bin:$PATH
```

4、Add configuration file

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

5、Start mongodb

```
/usr/local/mongodb/bin/mongod -f /data/appdb/conf/mongodb.conf
```

6、Configure mongodb password

```
# Login
mongo --port 27017
use admin

# Configured as username: root Password: pass123
db.createUser({user:"root",pwd:"pass123",roles:[{role:"root",db:"admin"}]})

# After the configuration is complete, log out and then log in again.
exit 

mongo --port 27017 -uroot -p pass123
```

**Step-4. Whaleal installation**

1、Gateway module

```
# Modify project configuration file server/ops-gateway-pro.yml
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Configure nacos address


# Start the network management module
nohup java -jar /root/whaleal/server/ops-gateway-1.0.0.jar --spring.config.location=ops-gateway-pro.yml > whaleal-geteway.log &
```



2、data collection module

```
# Modify project configuration file server/data-collection-api-dev.yml

spring:
  data:
    mongodb:
      uri: mongodb://****** # AppDB Database address
      database: ******
  application:
    name: data-os-collection
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Nacos address


# Start the data collection module
nohup java -jar /root/whaleal/server/data-collection-api-1.0.0.jar --spring.config.location=data-collection-api-pro.yml > data-collection-api.log &
```

3、web module

```
# Modify project configuration file server/ops-server-web-pro.yml

server:
  port: 9602
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Nacos address
  data:
    mongodb:
      uri: mongodb://****** # AppDB Database address
      database: ******
file:
  root:
    path: /home/whaleal/server/ # Whaleal Platform Database media package storage directory

# logging:
#   config: classpath:log4j2.yml



# Start the web module
nohup java -jar /root/whaleal/server/ops-server-web-1.0.0.jar --spring.config.location=ops-server-web-pro.yml  > ops-server-web.log &
```

4、Agent module

Copy agent-collection-1.0.0.jar to the file.root.path directory of the ops-server-web module

```
cp /root/whaleal/server/agent-collection-1.0.0.jar /home/whaleal/server/
```

**Step-5. All module startup and termination commands**

1、start up

```
nohup java -jar /root/whaleal/server/ops-gateway-1.0.0.jar --spring.confi
g.location=ops-gateway-pro.yml > whaleal-geteway.log &

nohup java -jar /root/whaleal/server/data-collection-api-1.0.0.jar --spring.config.location=data-collection-api-pro.yml > data-collection-api.log &

nohup java -jar /root/whaleal/server/ops-server-web-1.0.0.jar --spring.config.location=ops-server-web-pro.yml  > ops-server-web.log &
```

2、termination

```
ps  -ef | grep java | grep whaleal-server-web-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep data-collection-api-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep whaleal-gateway-1.0 | cut -c 9-15 | xargs kill -9
```

**Step-6. Front-end deployment Nginx**

[download link](http://nginx.org/download/), Download nginx installation package

1、lnstall dependent environment

```
yum install -y pcre pcre-devel zlib zlib-devel gcc++ gcc make
```

2、After downloading, unzip the nginx installation package

```
tar -zxvf nginx-1.21.1.tar.gz
```

3、Compile and install

```
cd nginx-1.21.1

./configure --prefix=/usr/local/nginx

make && make install

ln -s /usr/local/nginx/sbin/nginx /usr/local/sbin/
```

4、Start nginx

```
 nginx                  # start nginx
 nginx -s reload        # Restart nginx
 nginx -s stops         # Stop nginx
```

5、Configure front-end files

```
# Execute the following command to configure <gateway service external ip>

find  /usr/local/nginx/html -type f -exec sed -i 's/gateWayServer:8080/<Gateway service external ip>:8080/g' {} +


# Restart nginx
nginx -s reload
```

**Step-7. Browser access**

Browser access address：http://ip:8080/


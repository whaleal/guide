
## Whaleal-data安装部署

### 	服务器高可用部署

将服务在多个机器进行部署使用负载均衡器将流量分发到多个服务器上，以实现请求的平衡和分担。常见的负载均衡算法包括轮询、最少连接和哈希算法等。在系统中使用多个相同配置的服务器，以便在一个服务器发生故障时，其他服务器可以接管其工作并保持系统的连续性。常见的冗余备份模式包括主备模式、活动-活动模式和N+1模式等。


### 	程序包部署
#### 前端服务启动 
    源码编译后生成”dist”介质包。将 dist 介质包发送到服务器上。路径为 nginx 配置的介质包安装路径下
#### 重新启动 nginx 服务
    /usr/local/nginx/sbin/nginx -s reload -t

#### 后端服务启动
    源码编译后生成”filing-system-0.0.1-SNAPSHOT.jar”介质包。将该介质包上传至服务器。编辑配置文件：application.yml
#### 配置文件内容
```
server:
 port: 8000
spring:
 jackson:
 time-zone: GMT+8
 serialization:
 fail-on-empty-beans: false
 datasource:
 druid:
 type: com.alibaba.druid.pool.DruidDataSource
 driverClassName: com.mysql.jdbc.Driver
 url: jdbc:mysql://IP:3306/filing?characterEncoding=utf-8&useSSL=false
 username: root
 password: 123456
 initial-size: 5
 min-idle: 40
 max-active: 100
 max-wait: 5000
 time-between-eviction-runs-millis: 90000
 min-evictable-idle-time-millis: 1800000
 test-while-idle: true
 test-on-borrow: false
 test-on-return: false
 validation-query: SELECT 1
 filters: stat
 stat-view-servlet:
 url-pattern: /druid/*
 reset-enable: false
 enabled: true
 allow: 127.0.0.1
 web-stat-filter:
 url-pattern: /*
 exclusions: "*.js,*.gif,*.jpg,*.bmp,*.png,*.css,*.ico,/druid/*"
 redis:
 host: 127.0.0.1
 port: 6379
 timeout: 5000
 password: 123456
 elasticjob:
 zookeeper:
 server-lists: IP:2181
 namespace: epanasiashop-job-filing
 digest: zookeeper:Zkpp.x123
#jwt
jwt:
 header: Authorization
 secret: filingSecret!@#*
 expiration: 21600000
 online: online-token
 codeKey: code-key
generator:
 enabled: false
sso:
 clientId: TKDAP
 clientSecret: B7DuoJeqOGHvVWkPo7Nt
 # 回调地址
 redirectUri: http://:8080/login
 # 获取验证码
 authUri:
 # 登录第三方认证地址
 loginUri:
admin:
email: test@163.com #该邮箱为归档平台管理员邮箱。
allow-origin: http://127.0.0.1
loginCode:
 expiration: 2
mybatis-plus:
 mapper-locations: classpath:mapper/*.xml
 typeAliasesPackage: com.whaleal.filing.entity,com.whaleal.filing.model
 type-enums-package: com.whaleal.filing.enums
```
#### 修改完相应设置后 Java 介质包指定配置文件后台启动
启动命令：
```
nohup java -jar -Xms2048M -Xmx20000M -XX:PermSize=768M -XX:MaxPermSize=1536M -server -jar 
filing-system-0.0.1-SNAPSHOT.jar --spring.config.location=application.yml --jasypt.encryptor.password=SfXlqZmK4P257 &
```

#### 查看日志确认启动成功
    tail -f nohup.out

### 	docker容器快速部署
```
进入docker-compose.yml同级目录，使用 `docker-compose up -d`启动。

docker服务启动成功后，可通过`docker logs -f root_whaleal-data_1`命令查看whaleal-data服务运行日志。
本地服务器需绑定域名解析登录web端，命令：`sudo sh -c 'echo "docker服务器ip  whaleal-data.com" >> /etc/hosts'`

登录whaleal-data服务
`http://docker服务器ip` 或者`http://whaleal-data.com`

首次用户登录
user:"admin"
pwd:"123456"
系统强制要求用户修改密码后登录
```


Tips:
冷数据归档：
冷数据归档默认填写路径为/whalealdb.docker服务映射外部路径为/opt/whalealdb

### 	 快速访问

docker容器化启动whaleal-data服务。该服务依赖于`mysql`,`mongodb`,`redis`,`zookeeper`服务启动，通过`nginx`服务代理转发在本地浏览器中运行。

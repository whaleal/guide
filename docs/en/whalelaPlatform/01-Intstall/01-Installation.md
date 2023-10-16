## Installation

Whaleal Platform (WAP) supports the following two installation methods:
- VM Appliance
- Docker

#### VM Appliance

Step 1. Install JDK

a. Download JDK

Visit the [Oracle official website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to download an appropriate version of JDK for installation.

> Note:
>
> The following example uses jdk-8u151-linux-x64.tar.gz. If you download a different version, make sure the file extension is .tar.gz.

b. Create a directory

Execute the following command to create a `java` directory under the `/usr/` directory.

   ```
   mkdir /usr/java
   cd /usr/java
   ```

c. Copy the downloaded file `jdk-8u151-linux-x64.tar.gz` to the `/usr/java/` directory and unpack it.

   ```
   tar -zxvf jdk-8u151-linux-x64.tar.gz
   ```

d. Set environment variables

Edit the `/etc/profile` file and add the following content. Save the file afterward.

   ```bash
   # Set Java environment
   JAVA_HOME=/usr/java/jdk1.8.0_151
   JRE_HOME=/usr/java/jdk1.8.0_151/jre
   CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
   PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
   export JAVA_HOME JRE_HOME CLASS_PATH PATH
   ```

> Note:
>
> Make sure to adjust the paths for `JAVA_HOME` and `JRE_HOME` according to your actual installation paths and JDK version.

Apply the changes to the current session.

   ```
   source /etc/profile
   ```

e. Test

Test the JDK installation by running the following command.

   ```
   java -version
   ```

If it displays Java version information, the JDK is successfully installed:

   ```
   java version "1.8.0_151"
   Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
   Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
   ```

Step 2. Install NACOS

[Installation Guide](https://nacos.io/zh-cn/docs/cluster-mode-quick-start.html) - NACOS version 1.4 or higher is required.

Step 3. Install MongoDB

[Installation Guide]()

Step 4. Install Whaleal

a. Gateway Module

Modify the project configuration file `server/ops-gateway-dev.yml`:

```yaml
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Configure Nacos address
```

Start the gateway module:

```bash
nohup java -jar /root/whaleal/server/ops-gateway-1.0.0.jar --spring.config.location=ops-gateway-dev.yml > whaleal-geteway.log &
```

b. Data Collection Module

Modify the project configuration file `server/data-collection-api-dev.yml`:

```yaml
spring:
  data:
    mongodb:
      uri: mongodb://****** # Configure AppDB database address
      database: ******
  application:
    name: data-os-collection
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Configure Nacos address
```

Start the data collection module:

```bash
nohup java -jar /root/whaleal/server/data-collection-api-1.0.0.jar --spring.config.location=data-collection-api-dev.yml > data-collection-api.log &
```

c. Web Module

Modify the project configuration file `server/ops-server-web-dev.yml`:

```yaml
server:
  port: 9602
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Configure Nacos address
  data:
    mongodb:
      uri: mongodb://****** # Configure AppDB database address
      database: ******
file:
  root:
    path: /home/whaleal/server/ # Whaleal Platform database medium package storage directory
```

Start the web module:

```bash
nohup java -jar /root/whaleal/server/ops-server-web-1.0.0.jar --spring.config.location=ops-server-web-dev.yml  > ops-server-web.log &
```

d. Alert Module

Configure the project configuration file `server/ops-alert-dev.yml`:

```yaml
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Configure Nacos address
  data:
    mongodb:
      uri: mongodb://****** # Configure AppDB database address
      database: ******
feign:
  url: http://******/ # Whaleal project gateway address (http://IP:Port/)
```

Start the alert module:

```bash
nohup java -jar /root/whaleal/server/ops-alert-1.0.0.jar --spring.config.location=ops-alert-dev.yml > ops-alert.log &
```

e

. Archive Module

Configure the project configuration file `server/ops-archive-dev.yml`:

```yaml
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ****** # Configure Nacos address
  data:
    mongodb:
      uri: mongodb://****** # Configure AppDB database address
      database: ******
```

Start the archive module:

```bash
nohup java -jar /root/whaleal/server/ops-archive-1.0.0.jar --spring.config.location=ops-archive-dev.yml > ops-archive.log &
```

f. Third-Party Module

Configure the project configuration file `server/ops-third-party-dev.yml`:

```yaml
spring:
  cloud:
    nacos:
      discovery:
        server-addr: ******** # Configure Nacos address
  third:
    sms:
      host: http://****** # SMS platform address
      appcode: *** # AppCode
      from: *** # Sender's phone number
  mail:
    protocol: *** # Email service protocol
    port: ****** # Email server port
    host: ****** # Email platform address
    from: ****** # Email sender
    title: ****** # Email content title
    username: ****** # SMTP server account
    password: ****** # SMTP server password
    default-encoding: ******
    properties.mail.smtp.ssl.enable: ****** # Enable SSL transmission
    properties.mail.smtp.ssl.required: ****** # Require SSL transmission
    properties.mail.smtp.port: ****** # SMTP server port number
```

Start the third-party module:

```bash
nohup java -jar /root/whaleal/server/ops-third-party-1.0.0.jar --spring.config.location=ops-third-party-dev.yml > ops-third-party.log &
```

g. Agent Module

Copy `agent-collection-1.0.0.jar` to the `file.root.path` directory of the `ops-server-web` module:

```bash
cp /root/whaleal/server/agent-collection-1.0.0.jar /home/whaleal/server/
```

Step 5. Startup and Shutdown Commands for All Modules

Start

```bash
nohup java -jar /root/whaleal/server/ops-gateway-1.0.0.jar --spring.config.location=ops-gateway-dev.yml > whaleal-geteway.log &

nohup java -jar /root/whaleal/server/data-collection-api-1.0.0.jar --spring.config.location=data-collection-api-dev.yml > data-collection-api.log &

nohup java -jar /root/whaleal/server/ops-server-web-1.0.0.jar --spring.config.location=ops-server-web-dev.yml  > ops-server-web.log &

nohup java -jar /root/whaleal/server/ops-alert-1.0.0.jar --spring.config.location=ops-alert-dev.yml > ops-alert.log &

nohup java -jar /root/whaleal/server/ops-archive-1.0.0.jar --spring.config.location=ops-archive-dev.yml > ops-archive.log &

nohup java -jar /root/whaleal/server/ops-third-party-1.0.0.jar --spring.config.location=ops-third-party-dev.yml > ops-third-party.log &
```

Shutdown

```bash
ps  -ef | grep java | grep whaleal-server-web-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep data-collection-api-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep whaleal-alert-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep whaleal-third-party-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep agent-collection-1. | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep whaleal-archive-1.0 | cut -c 9-15 | xargs kill -9
ps  -ef | grep java | grep whaleal-gateway-1.0 | cut -c 9-15 | xargs kill -9
```

Step 6. Deploy Nginx for Front-End

Modify the Nginx configuration file:

```nginx
server {
    listen       ******; # External service port
    listen       ******; # Backend service address
    server_name  ******;

    location / {
        root   /www/dist; # Static files directory
        index  index.html index.htm;
    }
}
```

Restart Nginx:

```bash
nginx -s reload
```

Step 7. Access via Web Browser

Access the URL in the web browser: http://cloud.whaleal.com:8080/

#### Docker

Step 1. Install Docker

```bash
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun

# Restart the Docker service
systemctl restart docker
```

Step 2. Pull Docker Image

```bash
docker pull whaleal/whaleal:lstest
```

TODO: Start AppDB separately

Step 3. Run Docker Container

```bash
docker run -d -p 8080:8080 -p 9600:9600 whaleal
```

Step 4. Access via Web Browser

Access the URL in the web browser: http://IP:8080/dist/
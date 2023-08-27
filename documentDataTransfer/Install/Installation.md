## 安装部署

### 在CentOS部署DDT

#### JDK 安装

1. 下载 JDK11 版本的 tgz

```
    wget https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.9_linux-x64_bin.tar.gz
```

2. 解压下载tar包

```
   tar -zxvf jdk-11.0.9_linux-x64_bin.tar.gz
```

3. 更换目录

```
   mv jdk-11.0.9 /usr/local/jdk11
```

4. 配置环境变量

```
   vi /etc/profile
   export JAVA_HOME=/usr/lib/jvm/jdk11
   export JRE_HOME=${JAVA_HOME}/jre
   export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
   export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
```

5. 刷新生效

```
   source /etc/profile
```

6. 校验

```
   Java --version
```

#### 运行DDT

##### 前提条件

    需保证安装配置文件与java环境正常，才可启动DDT进程。

##### 运行服务

    进去bin目录
    执行启动：start-DDT.sh 脚本。启动传输数据功能
    执行启动：start-monitor.sh 脚本。启动web监控功能

##### 关闭服务

    进去bin目录
    执行启动: stop-DDT.sh 脚本。关闭传输数据功能
    执行启动：stop-monitor.sh 脚本。关闭web监控功能

#### DDT特性

    1. DDT支持全量，实时，全量和增量，全量和实时同步模式。 其中增量是指有时间范围限制的Oplog实时同步。
    2. 目前DDT支持3.2到6.0的MongoDB。新版本的时序表，桶表均可靠支持传输同步。
    3. 在实时同步期间，用户可以自定义同步某些DDL操作。同时DDL操作也会被记录在日志中，方便审查操作。

目前同版本同步数据无影响，高版本向低版本同步时，高版本新增类型无法同步至低版本，低版本向高版本同步时，高版本移除低版本的某些类型等无法同步。例如3.2版本删除了某索引，5.0版本新增了时序表等。

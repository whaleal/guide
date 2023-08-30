## JDK 安装部署

    Jdk 安装版本建议使用 jdk11.

### 1.依赖环境
    开源 jdk 需字体库支持，Linux 系统中已有则无需安装
    yum install fontconfig
    fc-cache --force
    fc-cache -f
### 2.解压 jdk 安装包
    tar -zxvf jdk-11.0.9_linux-x64_bin.tar.gz -C /usr/local/
### 3.配置环境变量
    vi /etc/profile
    最后一行添加以下配置
    export JAVA_HOME=/usr/local/jdk-11.0.9
    export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
    export PATH=$PATH:$JAVA_HOME/bin
    source /etc/profile 刷新配置使其生效
### 4.校验
    java –version
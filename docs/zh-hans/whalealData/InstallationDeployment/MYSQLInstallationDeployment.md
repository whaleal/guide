
## Mysql 安装部署
    Mysql 推荐使用版本 8.0
### 开放指定端口或关闭防火墙
#### 1. 查看已经开放的端口
       firewall-cmd --list-ports
#### 2.开放指定端口 
       firewall-cmd --zone=public --add-port=3306/tcp --permanent
#### 2. 重新加载防火墙配置
       firewall-cmd --reload
#### 3. 确认端口开放
       firewall-cmd --list-ports
#### 4. 关闭防火墙
       systemctl stop firewalld
#### 5. 确认防火墙状态
       systemctl status firewalld

### 基础环境准备

#### 1. 创建用户
       groupadd mysql
       useradd -r -g mysql -s /sbin/nologin mysql
#### 2. 安装 MySQL 需要的依赖
       yum install -y libncurses* libaio* lrzsz*
#### 3. 解压安装包
       tar -xvf mysql-8.0.28-linux-glibc2.12-x86_64.tar -C /usr/local/
#### 4. 修改文件名称
       mv mysql-8.0.28-linux-glibc2.12-x86_64/ mysql
#### 5. 创建所需目录
    cd /usr/local/mysql/
    创建数据目录
    mkdir data
#### 6. 修改目录权限
    chown -R mysql:mysql /usr/local/mysql/
    
### 部署 Mysql 服务
#### 1. 初始化数据库
    /usr/local/mysql/bin/mysqld --user=mysql --basedir=/usr/local/mysql/
    --datadir=/usr/local/mysql/data/ --initialize
    记录初始化 MySQL 服务密码
#### 2. 编辑 my.cnf
    [mysqld]
    basedir=/usr/local/mysql
    datadir=/usr/local/mysql/data
    socket=/usr/local/mysql/data/mysql.sock
    bind-address = 0.0.0.0
    user=root
    port=3306
    log-bin=mysql-bin
    server-id=1
    max_connections=2048
    character-set-server=utf8
    default-storage-engine=INNODB
    [client]
    socket=/usr/local/mysql/data/mysql.sock
#### 3. 配置环境变量
    echo "export PATH=$PATH:/usr/local/mysql/bin">> /etc/profile
    source /etc/profile
#### 4. 配置启动脚本
    复制 mysq 启动文件
    cp /usr/local/mysql/support-files/mysql.server /etc/rc.d/init.d/mysqld
    chmod +x /etc/rc.d/init.d/mysqld
    添加启动脚本
    cat > /lib/systemd/system/mysqld.service <<EOF
    [Unit]
    Description=mysqld
    After=network.target
    [Service]
    Type=forking
    ExecStart=/etc/rc.d/init.d/mysqld start
    ExecReload=/etc/rc.d/init.d/mysqld restart
    ExecStop=/etc/rc.d/init.d/mysqld stop
    PrivateTmp=true
    [Install]
    WantedBy=multi-user.target
    EOF
#### 5.重新加载配置文件
    systemctl daemon-reload
#### 6.设置开机自启动
    systemctl enable mysqld
#### 7.启动 mysql
    systemctl start mysqld
#### 8.查看 mysql 端口是否启动
    netstat -tunlp | grep 3306


### 配置密码远程连接
#### 1.输入刚刚打印出来的密码
    mysql -u root -p
#### 2.登陆成功后修改 root 密码
    ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';
#### 3.查看用户信息
    select user,host,ssl_type from mysql.user; use mysql;
#### 4.修改 host 字段为 %
    update user set host = '%' where user = 'root';
#### 5.刷新权限
    flush privileges;

### 添加归档平台字段
#### 1.登录 MySQL 数据库
    mysql -u root -p
#### 2.创建数据库
    create database filing;
#### 3.添加数据文件
    use filing;
    source /usr/local/filing.sql;
#### 4，查看数据
    use filing;
    show tables;
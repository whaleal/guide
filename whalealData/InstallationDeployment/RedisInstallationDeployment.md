## Redis 安装部署
### 开放指定端口或关闭防火墙
#### 1． 查看已经开放的端口
    firewall-cmd --list-ports
#### 2.开放指定端口 
    firewall-cmd --zone=public --add-port=6379/tcp --permanent
#### 3.重新加载防火墙配置
    firewall-cmd --reload
#### 4.确认端口开放
    firewall-cmd --list-ports
#### 5.关闭防火墙
    systemctl stop firewalld
#### 6.确认防火墙状态
    systemctl status firewalld
### 安装部署
#### 1. 解压安装包
    tar -zxvf redis-4.0.9.tar.gz -C /usr/local/
#### 2. 重命名
    mv redis-4.0.9 redis
#### 3. 安装依赖
    yum install gcc -y
#### 4. 编译文件
    make && make install
### 编辑配置文件
    vi redis.conf
#### 1. 设置密码
    requirepass foobared 修改
    requirepass 123456（设置密码为 123456）
#### 2. 后台启动
    daemonize no 修改
    daemonize yes（设置为后台启动）
#### 3. 远程访问
    bind 127.0.0.1 修改
    bind 0.0.0.0（设置为远程访问）
#### 4. 启动
    redis-server /usr/local/redis/redis.conf
#### 5. 校验
    redis-cli
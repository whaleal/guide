## Zookeeper 安装部署
### 开放指定端口或关闭防火墙
#### 1． 查看已经开放的端口
firewall-cmd --list-ports
#### 2.开放指定端口 
    firewall-cmd --zone=public --add-port=2181/tcp --permanent
#### 3.	 重新加载防火墙配置
    firewall-cmd --reload
#### 4.	 确认端口开放
    firewall-cmd --list-ports
#### 5.	 关闭防火墙
    systemctl stop firewalld
#### 6.	 确认防火墙状态
    systemctl status firewalld

### 安装部署
#### 1. 解压安装包
    tar -zxvf apache-zookeeper-3.6.1-bin.tar.gz -C /usr/local/
#### 2. 重命名文件
    mv apache-zookeeper-3.6.1-bin/ zookeeper
#### 3. 启动
    /usr/local/zookeeper/bin/zkServer.sh start /usr/local/zookeeper/conf/zoo_sample.cfg
#### 4. 校验
    /usr/local/zookeeper/bin/zkServer.sh status /usr/local/zookeeper/conf/zoo_sample.cfg
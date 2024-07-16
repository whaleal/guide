# Host Issues



### agent jar不能运行

- 当agent jar不能运行时首先检查自己主机有没有安装java环境，如没有安装则进行[java环境配置](../02-Usage/Server/EC2.md)。


### 主机异常宕机

- 每个被纳管进来的主机平台都会实时获取其主机状态，当平台显示主机异常宕机时首先查看主机是否正常运行，若主机异常关机等则进行物理主机的维修。
- 如果主机正常运行并没有宕机则查看agent进程是否正常运行，若进城崩溃或被异常kill进行重新启动即可。

### 不能连接Server

- 查看Server端是否正常
- 查看agent id是否正确并并重新运行


### 主机内存不足

- 当在主机创建集群时默认做大可用资源的二分之一，若不进行配置当集群创建过多时则会引起主机的崩溃宕机。
- 在创建集群时在高级配置中配置合适大小的cache size，以防止资源的占用与浪费。

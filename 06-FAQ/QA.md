

# 常见问题与解答

- ## whaleal平台支持哪些操作系统？

      本平台现阶段仅支持 centos 6，centos 7，centos 8，其余操作系统待开发。


- ## whaleal平台支持哪些数据库？

      现阶段仅支持mongoDB，其余数据库待开发。

- ## 我可以重置密码吗？

      普通用户不可以，可以找管理员重置密码。

- ## 如何添加新主机？

  - 添加新主机详情参考 
  [AddHost](../02-Usage/Host/AddHost.md)


- ## 如何创建集群？

  - 创建集群详情参考以下链接
  
    - 创建单节点[CreateStandalone](../02-Usage/MongoDB/CreateDeployment/CreateStandalone.md)
    - 创建复制集[CreateReplicaSet](../02-Usage/MongoDB/CreateDeployment/CreateReplicaSet.md)
    - 创建分片[CreateShardedCluster](../02-Usage/MongoDB/CreateDeployment/CreateShardedCluster.md)



- ## 告警条件意味着什么？

      告警条件是根据自身需求设置CPU、内存、交换、磁盘、带宽等阈值，当阈值被触发时会将异常情况发送给管理员用户。


- ## mongo之间支持同步吗？

      暂不支持，待开发。

- ## 支持哪些MongoDB认证方式？

      暂只支持账号密码。
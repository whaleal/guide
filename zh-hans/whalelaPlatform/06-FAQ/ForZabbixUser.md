## For Zabbix User

### WAP 是否支持创建 MongoDB 集群？

WAP 支持创建 MongoDB 集群：

1. 创建单节点：[CreateStandalone](../02-Usage/MongoDB/CreateDeployment/CreateStandalone.md)
2. 创建复制集集群：[CreateReplicaSet](../02-Usage/MongoDB/CreateDeployment/CreateReplicaSet.md)
3. 创建分片集群：[CreateShardedCluster](../02-Usage/MongoDB/CreateDeployment/CreateShardedCluster.md)



### WAP 是否支持纳管现有 MongoDB 集群？

WAP 支持对现有 MongoDB 集群的监控和管理。通过 [ExistingMongoDBDeployment](../02-Usage/MongoDB/CreateDeployment/ExistingMongoDBDeployment.md) 添加对 MongoDB 集群监控管理。

**WAP 支持通过一个节点配置，发现集群中所有节点并进行监控。**



### WAP 是否支持对 MongoDB 集群进行操作？

WAP 为用户提供了在使用、运维过程中常用的所有操作，促使用户在页面上可以通过配置、点击的方式完成对集群的变更。



### WAP 提供了哪些对于 MongoDB 的操作？

#### 诊断分析

通过实时诊断数据中Info、Health、Performance、LogVis、ExplainPlan结合分析，确认当前节点问题原因，得出解决方案。

#### 告警监控

通过配置告警参数阈值，在节点出现异常导致压力变大时，可以通过用户配置中邮箱、短信、钉钉等方式发送告警信息。

#### 数据管理

WAP 提供了页面展示框，展示用户自定义查询出数据的页面展示，方便、友好的展示数据。

#### 用户管理

展示集群中所有角色及用户，并详细展示角色及用户的权限。

#### 节点管理

用户可以通过 WAP 向复制集集群、分片集群shard/config中一键化添加节点，避免用户命令行方式输入错误导致添加失败。

#### 认证管理

用户可以通过 WAP 一键开启集群认证，WAP 以滚动方式重启集群，不影响服务使用。

#### 版本变更

WAP 提供滚动方式升降级操作，在不影响服务使用的情况下，对集群进行**相邻版本**之间的版本变更。

#### 架构变更

WAP 提供了 Standalone 架构变更为 ReplicaSet 架构功能。
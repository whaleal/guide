## Operation

```
Operation 可以执行以下操作：
 - Standalone to ReplicaSet
 - Cluster Info
 - Authentication
 - Modify Version
```

集群操作

a. 进入页面左侧导航栏

b. 点击 MongoDB 选项按钮，选择 MongoList 选项

c. 在 MongoDB 静态信息页面，点击类型为 “单实例” 的集群名

d. 在集群信息页面，选择操作

### Standalone to ReplicaSet

此操作可以将“单实例”集群转换为“复制集”集群，自动化配置，自动重启，减少用户操作步骤。

![image-20220721200526693](../../../../../images/whalealPlatformImages/MongoDB_Standalone_Operation_StandaloneToReplicaSet.png)

### Cluster Info

查看集群中节点配置信息

![image-20220721200313019](../../../../../images/whalealPlatformImages/MongoDB_Standalone_Operation_ClusterInfo.png)

### Authentication

开启认证，必须指定一个用户在admin库下

自动化创建用户、修改配置文件、重启服务操作。

![image-20220721200011007](../../../../../images/whalealPlatformImages/MongoDB_Standalone_Operation_Authentication.png)

### Modify Version

通过选择版本，对集群版本进行升降级操作，一键操作，修改FCV、更换介质包、重启服务。

![image-20220721195602291](../../../../../images/whalealPlatformImages/MongoDB_Standalone_Operation_ModifyVersion.png)
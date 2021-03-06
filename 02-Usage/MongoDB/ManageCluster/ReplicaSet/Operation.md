## Operation

```
Operation 可以执行以下操作：
 - Add Node
 - Cluster Info
 - Authentication
 - Modify Version
```

集群操作

a. 进入页面左侧导航栏

b. 点击 MongoDB 选项按钮，选择 MongoList 选项

c. 在 MongoDB 静态信息页面，点击类型为 “复制集” 的集群名

d. 在集群信息页面，选择操作

### Add Node

此操作可以向复制集集群中添加节点，并指定节点配置信息。

![image-20220722131146075](../../../../Images/MongoDB_Standalone_Operation_AddNode.png)

### Cluster Info

查看集群中节点配置信息

![image-20220722131415265](../../../../Images/MongoDB_ReplicaSet_Operation_ClusterInfo.png)

### Authentication

开启认证，必须指定一个用户在admin库下

自动化创建用户、修改配置文件、重启服务操作。

![image-20220722131557880](../../../../Images/MongoDB_ReplicaSet_Operation_Authentication.png)

### Modify Version

通过选择版本，对集群版本进行升降级操作，一键操作，修改FCV、更换介质包、重启服务。

![image-20220722131710063](../../../../Images/MongoDB_ReplicaSet_Operation_ModifyVersion.png)
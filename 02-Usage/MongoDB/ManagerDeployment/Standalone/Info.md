## Info Standalone

```
Manager Standalone 可以执行以下操作：
 - Monitoring Data
 - MongoDB Logs
 - Real-time Diagnosis
 - Alert
 - Details
 - Operation
```

查看 Standalon 节点数据

a. 进入页面左侧导航栏

b. 点击 MongoDB 选项按钮，选择 MongoList 选项

c. 在 MongoDB 静态信息页面，点击类型为 “单实例” 的集群名

### Monitoring Data

查看 Monitoring 数据

a. 在集群信息页面，选择节点信息

b. 在节点信息下，点击节点名称（一般为 hostname:端口）

Whaleal Platform 提供非常丰富的监控指标，并提供任意时间范围查询、过滤。

![image-20220721132736380](../../../../Images/MongoDB_Standalone_Monitor.png)



### MongoDB Logs

查看 MongoDB Logs 数据

a. 在集群信息页面，选择节点信息

b. 在节点信息下，点击查看日志

Whaleal Platform 记录并保存完整的 MongoDB 日志，提供过滤操作，遇到问题可以方便快速定位。

![image-20220721171530695](../../../../Images/MongoDB_Standalone_logs.png)



### Real-time Diagnosis

查看 Real-time Diagnosis 数据

a. 在集群信息页面，选择节点信息

b. 在节点信息下，点击实时诊断

**Top**

Top 展示当前时间点热集合。

![image-20220721172106803](../../../../Images/MongoDB_Standalone_Real_time_Top.png)



**Op**

Op 展示当前时间具体的操作命令执行

![image-20220721172328086](../../../../Images/MongoDB_Standalone_Real_time_Op.png)



**Explain**

Expliain 分析查询操作执行计划，方便调整、优化查询。

![image-20220721172503028](../../../../Images/MongoDB_Standalone_Real_time_Explain.png)



### Alert

查看 Alert 数据

a. 在集群信息页面，选择节点信息

b. 在节点信息下，点击告警监控

对特定指标进行告警配置，触发告警后，通过邮件、短信、钉钉等方式通知用户。

![image-20220721172846113](../../../../Images/MongoDB_Standalone_Alert.png)



### Details

查看 Details 数据

a. 在集群信息页面，选择节点信息

b. 在节点信息下，点击 Details

展示节点详细信息，包含：创建时间、版本、启动命令、节点配置信息等。

![image-20220721181402943](../../../../Images/MongoDB_Standalone_Details.png)



### Operation

对于此节点进行其他操作，包含：更新节点信息、启动节点、关闭节点、重启节点、脱离纳管、打开/关闭QPS监控、打开/关闭TopAndOp监控、打开/关闭MongoDBLog收集。

![image-20220721182045976](../../../../Images/MongoDB_Standalone_Operation.png)
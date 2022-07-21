# Mongo接口
接口调用时须在请求头中设置OPS-Token ，填写参数发起请求，返回内容为 JSON 格式的信息，返回特殊实体类将在最后提供实体类表格。
其参数为时间的都以时间戳形式传递。


有些接口调用时需用到clusterId、replicateId、eventId、mongoMemberId
~~~
eventId在"获取集群日志信息"接口处找到所需事件的id

mongoMemberId在“查找mongoDB集群信息数据”接口返回结果集中mongoMember集合中。

replicateId在“查找mongoDB集群信息数据”接口返回结果集中replicate集合中。

clusterId在“查找mongoDB集群信息数据”接口返回结果集中。
~~~


### 请求头默认格式，特殊情况特殊声明

    OPS-Token在调用登录接口时返回，在之后调用接口时将token放置请求头中。
[登录接口调用获取OPS-Token](Member.md)

| KEY                |     VALUE      |     
| -------------------|----------------------|
| Accept-Encoding        |         gzip, deflate, br |     
| Connection          |         keep-alive           |          
| Content-Type          |         application/json |    
| OPS-Token          |         "token"           |     
---


####  1 创建mongodb单例


1.1 请求路径：

POST https://192.167.3.200:9600/api/server/mongo/createMongoStandalone/{{isNewCluster}}/{{clusterId}}/{{replicateId}}


---

1.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| isNewCluster          |         path           |            是否时新集群            |        Yes       |Boolean
| clusterId          |         path           |            集群id            |        Yes       |String
| replicateId          |         path           |            复制集id            |        Yes       |String
| MongoMember          |         body           |            实例对象            |        yes       | 实体类
| tag          |         Params           |            标签            |        No       | String
~~~

{
"hostName": "chen",
"hostId": "62bbfbe9a46517610435d615",
"port": "25567",
"dataDirectory": "/home/chen/data25567",
"logFile": "/home/chen/log25567.log",
"version": "mongodb-linux-x86_64-rhel70-4.2.21",
"deleteDataAndLogAble": "false",
"authAble": "false",
"userName": "",
"password": "",
"configurationOptions": {
    "storage.wiredTiger.engineConfig.cacheSizeGB": "0.3"
    }
}
~~~

----

1.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |       int                |    
| msg       |         消息         |             string           |        
| eventId       |         事件id         |         string               |        
| data       |         返回数据         |          MongoMember              |        


~~~
{
    "msg": "正在执行",
    "eventId": "62ce9a7ded494511782ff392",
    "code": 1000,
    "data": {
        "id": null,
        "createTime": 0,
        "updateTime": 0,
        "memberName": "null:27017",
        "hostName": null,
        "hostId": null,
        "port": "27017",
        "version": null,
        "upgradeVersion": null,
        "userName": null,
        "password": null,
        "authDbName": "admin",
        "currentTimeMillis": 1657707133455,
        "dataDirectory": "/var/ops/mongodb1657707133455/data/",
        "logFile": "/var/ops/mongodb1657707133455/log/log.log",
        "confPath": "/var/ops/mongodb1657707133455/mongo.conf",
        "deleteDataAndLogAble": false,
        "authAble": false,
        "runShCmd": null,
        "type": 11,
        "status": "无状态",
        "monitorServerStatus": false,
        "monitorTopAndOp": false,
        "collectMongoLog": false,
        "mongoLogFileOffset": 0,
        "operaLogTemp": [],
        "votes": 1,
        "priority": 1.0,
        "delay": 0,
        "buildIndexes": true,
        "procId": "",
        "clusterId": "62ce9a7ded494511782ff393",
        "replId": null,
        "clusterName": null,
        "tags": {},
        "configurationOptions": {},
        "operateVersion": 0
    }
}
~~~
---
---
####  2 单节点转为复制集.



2.1 请求路径：

GET http://192.167.3.200:9600/api/server/mongo/standaloneToReplicate/{{clusterId}}

---

2.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String        |


![postman_mongo_standaloneToReplicate](../Images/standaloneToReplicate.png)
----

2.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |            int           |    
| msg       |         返回消息         |           string             |        

![postman_mongo_standaloneToReplicate_result](../Images/standaloneToReplicate_r.png)
---


####  3 创建mongodb复制集



3.1 请求路径：

POST http://{Server-Host}:{端口}/api/server/mongo/createMongoReplica/{{isNewCluster}}

---

3.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| isNewCluster          |         Path           |            集群id            |        Yes       |String        |
| mongoReplica          |         body           |           mongoReplica           |        yes       |实体类        |
| tag          |         params           |            标签            |        No       |String        |

~~~
{
    "userName": "",
    "password": "",
    "type": 1,
    "clusterId": "",
    "replicaName": "qaq",
    "deleteDataAndLogAble": false,
    "status": "",
    "authAble": "false",
    "operaLog": [],
    "memberList": [
        {
           ...
    ],
    "replicationSettings": {
        "protocolVersion": null,
        "chainingAllowed": null,
        "writeConcernMajorityJournalDefault": null,
        "heartbeatTimeoutSecs": null,
        "electionTimeoutMillis": null,
        "catchUpTimeoutMillis": null,
        "catchUpTakeoverDelayMillis": null,
        "getLastErrorDefaults": null,
        "forceReconfigure": null
    }
}
~~~
----

3.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |           int            |    
| data       |         返回数据         |         MongoReplica               |        
| msg       |         返回消息         |         string               |        
| eventId       |         事件ID         |          string              |        

~~~
{
    "msg": "正在执行",
    "eventId": "62cf7903ed494511782ff4fa",
    "code": 1000,
    "data": {
        "id": null,
        "createTime": 0,
        "updateTime": 0,
        "replicaName": null,
        "memberList": [],
        "type": 1,
        "clusterId": "62cf7903ed494511782ff4f9",
        "deleteDataAndLogAble": false,
        "status": null,
        "operaLog": [],
        "replicationSettings": {},
        "replicationOtherSettings": {},
        "authAble": false,
        "userName": null,
        "password": null,
        "authDbName": "admin",
        "protocolVersion": 1,
        "writeConcernMajorityJournalDefault": false
    }
}
~~~
---

####  4 创建mongodb分片



4.1 请求路径：

POST http://{Server-Host}:{端口}/api/server/mongo/createMongoSharded/{{isNewCluster}}

---

4.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| isNewCluster          |         Path           |            文件名称            |        Yes       |String        |
| mongoShard          |         body           |            mongoShard            |        yes       |mongoShard        |
| tag          |         params           |            文件名称            |        No       |String        |


~~~


{
    "clusterName": "fenpian",
    "deleteDataAndLogAble": "false",
    "authAble": "false",
    "userName": "",
    "password": "",
    "shardingMap": {
        "shard1": {
            "memberList": [
                ...
            ],
            "replicationSettings": {
               ...
            }
        }
    },
    "config": {
        "memberList": [
           ...
        ],
        "replicationSettings": {
            ...
        }
    },
    "mongoS": [
        ...
    ]
}
~~~
----

4.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |      int                 |    
| msg       |         返回消息         |         string               |        
| eventId       |         事件id         |      string                  |        
| data       |         返回数据         |      MongoShard                  |        

~~~
{
    "msg": "正在执行",
    "eventId": "62cf8e51ed494511782ff6c9",
    "code": 1000,
    "data": {
        "id": null,
        "createTime": 0,
        "updateTime": 0,
        "clusterName": null,
        "clusterId": "62cf8e51ed494511782ff6c8",
        "config": null,
        "mongoS": [],
        "shardingMap": {},
        "operaLog": [],
        "deleteDataAndLogAble": false,
        "authAble": false,
        "userName": null,
        "password": null,
        "authDbName": "admin",
        "status": null
    }
}
~~~
---

####  5 操作开启认证的集群



5.1 请求路径：

POST http://{Server-Host}:{端口}/api/server/mongo/operateClusterAbleAuth/{{clusterId}}

---

5.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            文件名称            |        Yes       |String        |
| map          |         body           |           传参            |        Yes       |map        |


![postman_mongo_operateClusterAbleAuth](../Images/operateClusterAbleAuth.png)
----

5.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |          int             |    
| msg       |         返回消息         |            string            |        
| eventId       |         事件id         |        string                |        

![postman_mongo_operateClusterAbleAuth_result](../Images/operateClusterAbleAuth_r.png)
---

####  6 添加shard



6.1 请求路径：

POST http://{Server-Host}:{端口}/api/server/mongo/addShard/{{clusterId}}

---

6.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         path           |            集群id            |        Yes       |String        |
| mongoReplica          |         body           |            实体类            |        Yes       |mongoReplica        |


~~~

{
    "type": 3,
    "clusterId": "",
    "replicaName": "qwe",
    "authAble": "true",
    "userName": "",
    "password": "",
    "deleteDataAndLogAble": false,
    "status": "",
    "operaLog": [],
    "memberList": [
        {
            "type": 51,
            "hostName": "chen",
            "hostId": "62bbfbe9a46517610435d615",
            "port": "44453",
            "version": "mongodb-linux-x86_64-rhel70-4.2.21",
            "votes": "1",
            "priority": "1",
            "delay": "",
            "buildIndexes": true,
            "dataDirectory": "/home/chen/data44453",
            "logFile": "/home/chen/log44453.log",
            "configurationOptions": {
                "storage.wiredTiger.engineConfig.cacheSizeGB": "0.3"
            }
        }
    ]
}
~~~

----

6.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |    
| msg       |         返回消息         |          string              |        

![postman_mongo_addShard_result](../Images/addShard_r.png)
---



####  7 纳管集群信息



7.1 请求路径：

POST http://{Server-Host}:{端口}/api/server/mongo/mongoManaged

---

7.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|        mongoMember    |        body             |           实体类              |     yes           |   mongoMember      |

![postman_mongo_mongoManaged](../Images/mongoManaged.png)



----

7.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |          int             |    
| msg       |         返回消息         |       string                 |        
| data       |         返回数据         |         MongoClusterInformation               |        

~~~
{
    "msg": "正在执行",
    "code": 1000,
    "data": {
        "id": "62cfa41fed494511782ff7a2",
        "createTime": 1657775135326,
        "updateTime": 1657775135326,
        "clusterName": "fp",
        "type": 1,
        "mongoMember": {
            ...
        },
        "mongoReplica": null,
        "mongoShard": null,
        "status": null,
        "fcv": null,
        "tag": null,
        "create": true
    }
}

~~~

####  8 升降级



8.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/upgrade/{{clusterId}}/{{version}}/{{type}}

---

8.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         path           |            集群id            |        Yes       |String        |
| version          |         path           |            版本            |        Yes       |String        |
| type          |         path           |            集群类型            |        Yes       |String        |


![postman_mongo_upgrade](../Images/upgrade.png)


----

8.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| msg       |         返回消息         |         string               |        

![postman_mongo_upgrade_result](../Images/upgrade_r.png)



---
####  9 针对节点进行操作.



9.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/operate/{{clusterId}}/{{mongoMemberId}}/{{operateType}}/{{mongoMemberName}}

---

9.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         path           |            集群id            |        Yes       |String        |
| mongoMemberId          |         path           |            mongo集群id            |        Yes       |String        |
| operateType          |         path           |            操作类型            |        Yes       |String        |
| mongoMemberName          |         path           |            mongo集群名称            |        Yes       |String        |

![postman_mongo_operate](../Images/operate_Single.png)


----
9.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |    
| msg       |         返回消息         |         string               |        

![postman_mongo_operate_result](../Images/operate_Single_r.png)


---
####  10 针对集群进行操作



10.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/operate/{{clusterId}}/{{operateType}}

---

10.2 请求参数：


    operateType：updateMongoMemberInfo，startUp，shuntDown，restart，delete

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         path           |            集群id            |        Yes       |String        |
| operateType          |         path           |            操作类型            |        Yes       |String        |

![postman_mongo_operate](../Images/operate_cluster.png)


----

10.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| msg       |         返回消息         |            string            |     

![postman_mongo_operate_result](../Images/operate_cluster_r.png)



####  11 更新集群信息



11.1 请求路径：

POST http://{Server-Host}:{端口}/api/server/mongo/updateClusterInfo

---

11.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| MongoClusterInformation          |         body           |            实体类            |        Yes    | MongoClusterInformation          |         body           |            实体类            |        Yes       |mongoReplica        |
|


~~~
{
    "id": "62cfa574ed494511782ff7c1",
    "createTime": 1657775520238,
    "updateTime": 1657775520238,
    "clusterName": "chen:63343",
    "type": 1,
    "mongoMember": {
        "id": "62cfa574ed494511782ff7c1",
        "createTime": 1657775520238,
        "updateTime": 1657776654587,
        "memberName": "chen:63343",
        "hostName": "chen",
        "hostId": "62bbfbe9a46517610435d615",
        "port": "63343",
        "version": "4.2.21",
        "upgradeVersion": null,
        "userName": "",
        "password": "",
        "authDbName": "admin",
        "currentTimeMillis": 1657775476157,
        "dataDirectory": "/home/chen/data63343",
        "logFile": "/home/chen/log63343.log",
        "confPath": "/home/chen/data63343/chen_63343.conf",
        "deleteDataAndLogAble": false,
        "authAble": false,
        "runShCmd": "/var/ops/agent//mongodb-linux-x86_64-rhel70-4.2.21/bin/mongod -f /home/chen/data63343/chen_63343.conf",
        "type": 11,
        "status": "正在运行",
        "monitorServerStatus": false,
        "monitorTopAndOp": false,
        "collectMongoLog": false,
        "mongoLogFileOffset": 0,
        "operaLogTemp": [],
        "votes": 1,
        "priority": 1,
        "delay": 0,
        "buildIndexes": true,
        "procId": "10654",
        "clusterId": "62cfa574ed494511782ff7c1",
        "replId": null,
        "clusterName": null,
        "tags": {},
        "configurationOptions": {
            "systemLog_destination": "file",
            "storage_wiredTiger_engineConfig_cacheSizeGB": "0.3",
            "systemLog_path": "/home/chen/log63343.log",
            "processManagement_fork": "true",
            "storage_dbPath": "/home/chen/data63343",
            "systemLog_logAppend": "true",
            "net_bindIp": "0.0.0.0",
            "net_port": "63343"
        },
        "operateVersion": 80
    },
    "mongoReplica": null,
    "mongoShard": null,
    "status": "正常",
    "fcv": "4.2",
    "tag": "",
    "create": true
}
~~~

----

11.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |          int             |    
| msg       |         返回消息         |             string           |        


![postman_mongo_updateClusterInfo_result](../Images/updateClusterInfo_r.png)




---
---


## MongoMember


|       Name         |     Type             |    Description      |   
| ------------       |----------            |---------------------|
| memberName                 |   string             |         主机名:端口          |   
| hostName             |   string             |         主机名     |   
| hostId              |   Long |         主机id     |   
| port               |   string             |         端口     |   
| version         |   string             |         版本     |   
| upgradeVersion           |   string             |         升降级版本     |   
| password           |   string             |         节点密码     |   
| authDbName           |   string             |         认证库     |   
| currentTimeMillis           |   long             |         当前时间戳     |   
| dataDirectory           |   string             |         数据目录     |   
| userName             |   string             |         节点用户名     |   
| logFile             |   string             |         日志文件     |   
| confPath             |   string             |         配置文件路径     |   
| deleteDataAndLogAble             |   string             |         是否强制删除     |   
| authAble             |   string             |         是否开启认证     |   
| runShCmd             |   string             |         执行启动命令     |   
| type             |   enum             |         节点类型     |   

注 type:11 单例
* 
* <p> 普通复制集
* 31 普通成员节点

* 32 隐藏节点
* 33 仲裁节点
* 34 隐藏延迟节点
* 35 主节点
* <p> config复制集
* 41 config普通成员节点
* 42 config隐藏节点
* 43 config仲裁节点
* 44 config隐藏延迟节点
* 45 config主节点
* <p> shard复制集
* 51 shard普通成员节点
* 52 shard隐藏节点
* 53 shard仲裁节点
* 54 shard隐藏延迟节点
* 55 shard主节点
* <p> mongoS
* 61 mongoS

---
---





## MongoReplica


|       Name         |     Type             |    Description      |   
| ------------       |----------            |---------------------|
| replicaName                 |   string             |         集群名          |   
| memberList             |   List<MongoMember>             |         成员列表     |   
| type              |   enum |         大小     |   
| clusterId               |   string             |         所属集群id     |   
| deleteDataAndLogAble         |   boolean             |         是否强制删除已经存在的数据目录和日志文件     |   
| status           |   string             |         状态     |   
| operaLog             |   List<String             |         复制集操作日志     |   
| replicationSettings             |   Map<String, Object>             |         复制集高级配置     |   
| replicationOtherSettings             |   Map<String, Object>             |         其他附加配置信息     |   
| authAble             |   boolean             |         是否开启认证     |   
| userName             |   string             |         节点用户名     |   
| password             |   string             |         节点密码     |   
| authDbName             |   string             |         认证库     |   
| protocolVersion             |   long             |         协议版本     |   
| writeConcernMajorityJournalDefault             |   boolean             |         是否默认投票     |   
type:
* 普通复制集 1
* config 2
* shard 3


---
---

## MongoShard


|       Name         |     Type             |    Description      |   
| ------------       |----------            |---------------------|
| clusterName                 |   string             |         集群名          |   
| clusterId             |   string             |         所属集群id     |   
| config              |   MongoReplica |         config复制集     |   
| mongoS               |   List<MongoMember>             |         mongoS列表     |   
| shardingMap         |   Map<String, MongoReplica>             |         shard集合     |   
| operaLog           |   List<String>             |         分片操作日志     |   
| deleteDataAndLogAble             |   boolean             |         是否强制删除     |   
| authAble             |   boolean             |         是否开启认证     |   
| userName             |   string             |         节点用户名     |   
| password             |   string             |         节点密码     |   
| authDbName             |   string             |         认证库     |   
| status             |   string             |         状态     |   


---
---



## MongoClusterInformation


|       Name         |     Type             |    Description      |   
| ------------       |----------            |---------------------|
| clusterName                 |   string             |         集群名          |   
| type             |   int             |         类型     |   
| mongoMember              |   MongoMember |         单例     |   
| mongoReplica               |   MongoReplica             |         复制集     |   
| mongoShard         |   MongoShard             |         分片     |   
| isCreate           |   boolean             |         默认新建的集群信息     |   
| status             |   string             |         集群状态     |   
| fcv             |   string             |         fcv     |   
| tag             |   string             |         标签     |   

 status：
* 集群状态
* 正常
* 异常
* 关机
* 脱离纳管

type:
* 1 单例
* 2 复制集
* 3 分片



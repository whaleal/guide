# MongoDBData接口

接口调用时须在请求头中设置OPS-Token ，填写参数发起请求，返回内容为 JSON 格式的信息，返回特殊实体类将在最后提供实体类表格。
其参数为时间的都以时间戳形式传递。


有些接口调用时需用到nodeId、mongoMemberId、clusterId、eventId
~~~
nodeId即mongoMemberId 在“查找mongoDB集群信息数据”接口返回结果集中data集合的中mongo集合的“id”

eventId在"获取集群日志信息"接口处找到所需事件的id

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
---




###  1 获取mongodb集群信息

## Deprecated 已弃用

1.1 请求路径：




GET http://{Server-Host}:{端口}/api/server/mongo/monitor/project/data/{{clusterName}}/{{projectType}}

---

1.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterName          |         Path           |            集群名称            |        Yes       |String
| projectType          |         Path           |            类型            |        Yes       |String




----

<br>


###  2 获取群集大小前五名


2.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/monitor/cluster/size/top/five

---

2.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| beginTime          |         Params           |            开始时间            |        Yes       |long
| endTime          |         Params           |            结束时间            |        Yes       |long

<br>



![img.png](../Images/cluster_size_top_five.png)

----

2.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |             int          |    
| data       |         返回数据         |         List                |        

<br>

[comment]: <> (![img.png]&#40;../Images/cluster_size_top_five_r.png&#41;)

~~~
{
    "code": 1000,
    "data": [
        {
            "_id": "62d666c50f57845ee4c76090",
            "clusterSize": 0,
            "size": "0.00KB",
            "clusterName": "test_repl"
        },
        {
            "_id": "62d65068561b4a25b8339740",
            "clusterSize": 0,
            "size": "0.00KB",
            "clusterName": "shard"
        }
    ]
}

~~~

---

<br>



###  3 获取集合大小前五名


3.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/monitor/collection/size/top/five

---

3.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| beginTime          |         Params           |            开始时间            |        Yes       |long
| endTime          |         Params           |            结束时间            |        Yes       |long

<br>



![img_1.png](../Images/collection_size_top_five.png)

----

3.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据         |        List                |        

<br>


[comment]: <> (![img_1.png]&#40;../Images/collection_size_top_five_r.png&#41;)

~~~
{
    "code": 1000,
    "data": [
        {
            "_id": "62d67d21239d00094230b08f",
            "clusterId": "62d67d21239d00094230b08f",
            "createTime": 1658394516783,
            "dbTables": {
                "name": "fs.chunks",
                "type": "collection",
                "options": {},
                "info": {
                    "readOnly": false,
                    "uuid": {
                        "type": 4,
                        "data": "8MfjmDBFR5q9BYztGFDJQQ=="
                    }
                },
                "idIndex": {
                    "v": 2,
                    "key": {
                        "_id": 1
                    },
                    "name": "_id_",
                    "ns": "test.testColl"
                },
                "storageSize": 20,
                "size": 0,
                "ns": "test.testColl"
            },
            "fromServerExe": false,
            "updateTime": 0,
            "clusterName": "shard",
            "dbName": "test",
            "collectionName": "testColl",
            "size": "0.00KB"
        }
    ]
}
~~~

---

<br>



###  4 获取QPS大小前五


4.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/monitor/QPS/size/top/five

---

4.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| beginTime          |         Params           |            开始时间            |        Yes       |long
| endTime          |         Params           |            结束时间            |        Yes       |long


<br>


![img_2.png](../Images/QPS_size_top_five.png)

----

4.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |            int           |    
| data       |         返回数据         |          List              |        

<br>

[comment]: <> (![img_2.png]&#40;../Images/QPS_size_top_five_r.png&#41;)

~~~
{
    "code": 1000,
    "data": [
        {
            "_id": {
                "hostId": "62cbbd7607bebb71b8429e5e",
                "port": "47018"
            },
            "host": "server200",
            "port": "47018",
            "QPS": 5520,
            "instance": "server200:47018"
        }
    ]
}
~~~

---

<br>



###  5 获取连接实例前五


5.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/monitor/connection/instance/top/five

---

5.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| beginTime          |         Params           |            开始时间            |        Yes       |long
| endTime          |         Params           |            结束时间            |        Yes       |long

<br>



![img_3.png](../Images/connection_size_top_five.png)

----

5.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |      int                 |    
| data       |         返回数据         |        List                |        

<br>

[comment]: <> (![img_3.png]&#40;../Images/connection_size_top_five_r.png&#41;)

~~~
{
    "code": 1000,
    "data": [
        {
            "_id": {
                "hostId": "62cbbd7607bebb71b8429e5e",
                "port": "47018"
            },
            "host": "server200",
            "port": "47018",
            "Conn": 76,
            "instance": "server200:47018"
        }
    ]
}
~~~

---

<br>


###  6 获取慢查询前五


6.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/monitor/slowest/instance/top/five

---

6.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| beginTime          |         Params           |            开始时间            |        Yes       |long
| endTime          |         Params           |            结束时间            |        Yes       |long

<br>



![img_4.png](../Images/slowest_size_top_five.png)

----

6.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |          int             |    
| data       |         返回数据         |           List             |        

<br>

[comment]: <> (![img_4.png]&#40;../Images/slowest_size_top_five_r.png&#41;)

~~~
{
    "code": 1000,
    "data": [
        {
            "_id": "62d66d3cc5b6206027b993b0",
            "slow count": 8,
            "instance": "server200:47018"
        }
    ]
}
~~~

---

<br>


###  7 节点实时监控信息

            
7.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/monitor/data/{{nodeId}}/{{type}}

---

7.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| nodeId          |         Path           |            节点id            |        Yes       |String
| type          |         Path           |            查询类型            |        Yes       |String
| timeGranularity          |         Params           |            时间粒度            |        Yes       |long
| startTimeForTimeInterval          |         Params           |            开始时间间隔            |        Yes       |long
| endTimeForTimeInterval          |         Params           |            结束时间间隔            |        Yes       |long

<br>


![img_2.png](../Images/monitor_data.png)

----

7.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |            int           |    
| data       |         返回数据         |            List            |        


<br>

[comment]: <> (![img_5.png]&#40;../Images/monitor_data_r.png&#41;)

~~~
 {
    "code": 1000,
    "data": {
        "createTimeList": [],
        "size": 0,
        "metrics": [
            {
                "qps": {
                    "query": [],
                    "getMore": [],
                    "insert": [],
                    "update": [],
                    "message": {
                        "insert": "The average rate of inserts performed per second over the selected sample period",
                        "delete": "The average rate of deletes performed per second over the selected sample period",
                        "update": "The average rate of updates performed per second over the selected sample period",
                        "query": "The average rate of queries performed per second over the selected sample period",
                        "command": "The average rate of commands performed per second over the selected sample period",
                    },
                    "delete": [],
                    "command": []
                }
            }
            ...
        ]
    }
}
~~~

---

<br>




###  8 根据id查询集群信息


8.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoCluster/{{clusterId}}

---

8.2 请求参数：



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String

<br>



![img_1.png](../Images/getMongoCluster.png)


----

8.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |           int            |    
| data       |         返回数据         |          List              |        

<br>

[comment]: <> (![img_6.png]&#40;../Images/getMongoCluster_r.png&#41;)

~~~
{
    "code": 1000,
    "data": {
        "id": "62d67d21239d00094230b08f",
        "createTime": 1658223967052,
        "updateTime": 1658223967052,
        "clusterName": "test",
        "type": 2,
        "mongoMember": null,
        "mongoReplica": {
            "id": "62d67d21239d00094230b08f",
            "createTime": 0,
            "updateTime": 0,
            "replicaName": "test",
            "memberList": [
              
              ...
            ],
            "type": 1,
            "clusterId": "62d67d21239d00094230b08f",
            "deleteDataAndLogAble": false,
            "status": "正在运行",
            "operaLog": [],
            "replicationSettings": {},
            "replicationOtherSettings": {
                "securityKeyFileValue":
            },
            "authAble": true,
            "userName": "root",
            "password": "123456",
            "authDbName": "admin",
            "protocolVersion": 1,
            "writeConcernMajorityJournalDefault": false
        },
        "mongoShard": null,
        "status": "正常",
        "fcv": "4.2",
        "tag": "ys",
        "create": true
    }
}
~~~

---


<br>




###  9 获取集群日志信息


9.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoClusterLogData/{{clusterId}}/{{pageIndex}}/{{pageSize}}

---

9.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |int
| pageIndex          |         Path           |            第几页            |        Yes       |int
| pageSize          |         Path           |            每页大小            |        Yes       |String
| memberName          |         Params           |            节点名称            |        No       |String
| logContent          |         Params           |            日志内容            |        No       |String
| startTime         |         Params           |            开始时间            |        No       |long
| endTime         |         Params           |            结束时间            |        No       |long

<br>


![img_2.png](../Images/getMongoClusterLogData.png)


----

9.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |           int            |    
| data       |         返回数据         |             List           |        

<br>

[comment]: <> (![img_8.png]&#40;../Images/getMongoClusterLogData_r.png&#41;)

~~~
{
    "code": 1000,
    "data": [
        {
            "id": "62d4f0363e50046ce51d44f3",
            "createTime": 1658122294338,
            "updateTime": 1658122294338,
            "memberName": "cluster",
            "clusterId": "62d4bdfd3e50046ce51d41f6",
            "eventId": null,
            "logInfoList": [
                {
                    "createTime": 1658122294338,
                    "log": "rz集群操作[updateMongoMemberInfo]成功"
                }
            ]
        }
    ]
}
~~~
 


---

<br>



###  10 获取mongo集群日志数


10.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoClusterLogCount/{{clusterId}}

---

10.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String
| memberName          |         Params           |            节点名称            |        Yes       |String
| logContent          |         Params           |            日志内容            |        Yes       |String
| startTime          |         Params           |            开始时间            |        Yes       |long
| endTime          |         Params           |            结束时间            |        Yes       |long

<br>



![img_3.png](../Images/getMongoClusterLogCount.png)

----

10.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |            int|    
| data       |         返回数量         |           int             |        

<br>


![img_4.png](../Images/getMongoClusterLogCount_r.png)

---

<br>


###  11 查询mongoD的日志信息.


11.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoDLogData/{{mongoMemberId}}/{{pageIndex}}/{{pageSize}}

---

11.2 请求参数：

    type类型：为空时查询全部，STORAGE，RECOVERY，CONTROL

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| mongoMemberId          |         Path           |            mongo服务id            |        Yes       |String
| pageIndex          |         Path           |            第几页            |        Yes       |int
| pageSize          |         Path           |            每页大小            |        Yes       |int
| type          |         Params           |            类型            |        No       |String
| startTime          |         Params           |            开始时间            |        No       |long
| endTime          |         Params           |            结束时间            |        No       |long
| content          |         Params           |            内容            |        No       |String

<br>



![img_5.png](../Images/getMongoDLogData.png)

----

11.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据         |          MongoMember              |        


~~~
{
    "code": 1000,
    "data": [
        {
            "id": "62d5037fbb551e67507f9a32",
            "createTime": 0,
            "updateTime": 0,
            "log": {
                "t": "2022-07-18T06:53:49.151+00:00",
                "s": "I",
                "c": "NETWORK",
                "id": "[conn3161]",
                "msg": "end connection 192.168.3.80:58778 (5 connections now open)"
            },
            "nodeId": "62d4be9d3e50046ce51d4228",
            "fileOffset": 0
        }
    ]
}
~~~

---

<br>


###  12 查询mongoD的日志信息数


12.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoDLogCount/{{mongoMemberId}}

---

12.2 请求参数：

    type类型：为空时查询全部，STORAGE，RECOVERY，CONTROL

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| mongoMemberId          |         Path           |            mongo节点id            |        Yes       |String
| type          |         Params           |            类型            |        Yes       |String
| startTime          |         Params           |            开始时间            |        Yes       |String
| endTime          |         Params           |            结束时间            |        Yes       |String
| content          |         Params           |            搜索内容            |        Yes       |String

<br>


![img_6.png](../Images/getMongoDLogCount.png)



----

12.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |    
| data       |         返回数量         |          int              |        

<br>



![img_7.png](../Images/getMongoDLogCount_r.png)



---

<br>


###  13 获取mongo的 top与op


13.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoTopAndOp/{{mongoMemberId}}/{{type}}

---

13.2 请求参数：



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| mongoMemberId          |         Path           |            集群id            |        Yes       |String
| type          |         Path           |            类型：1 top,    2 op            |        Yes       |String

<br>


![img_8.png](../Images/getMongoTopAndOp.png)


----

13.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int|    
| data       |         返回数据         |           List             |        

<br>



![img_9.png](../Images/getMongoTopAndOp_r.png)


---

<br>


###  14 更新集群名称


14.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/updateClusterName/{{clusterId}}/{{newClusterName}}

---

14.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String
| newClusterName          |         Path           |            新名称           |        Yes       |String

<br>


![img_10.png](../Images/updateClusterName.png)


----

14.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |    
| msg       |         返回消息         |            String            |        

<br>

![img_11.png](../Images/updateClusterName_r.png)


---

<br>


###  15 获取mongo统计信息


15.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoStatistics

---

15.2 请求：


![img_12.png](../Images/getMongoStatistics.png)


----

15.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据         |          List              |      

<br>


![img_13.png](../Images/getMongoStatistics_r.png)


---

<br>


###  16 根据事件id查询mongo事件


16.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/findMongoEventLogByEventId/{{eventId}}

---

16.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| eventId          |         Path           |            事件id            |        Yes       |String

<br>


![img_14.png](../Images/findMongoEventLogByEventId.png)


----

16.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据         |          List              |       

<br>


[comment]: <> (![img_15.png]&#40;../Images/findMongoEventLogByEventId_r.png&#41;)


~~~
{
    "code": 1000,
    "data": [
        {
            "createTime": 1658131316409,
            "log": "chen:45463操作[openQPS]成功"
        },
        {
            "createTime": 1658131317418,
            "log": "事件组结束"
        }
    ]
}
~~~

---

<br>


###  17 获取mongo事件日志数据


17.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoEventLogData/{{clusterId}}/{{pageIndex}}/{{pageSize}}

---

17.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String
| pageSize          |         Path           |           每页大小            |        Yes       |int
| pageIndex          |         Path           |          第几页             |        Yes       |int
| status          |         Params           |          状态            |        No       |String
| eventName          |         Params           |       事件名称                |        No       |String
| operatorName          |         Params           |       操作者                |        No       |String

<br>


![img_16.png](../Images/getMongoEventLogData.png)


----

17.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |    
| data       |         返回数据         |      List                  |      


<br>

[comment]: <> (![img_14.png]&#40;../Images/getMongoEventLogData_r.png&#41;)

~~~
{
    "code": 1000,
    "data": [
        {
            "id": "62d5281602d41247cf3741d0",
            "createTime": 1658136598663,
            "updateTime": 1658136704891,
            "clusterId": "62d4bdfd3e50046ce51d41f6",
            "eventName": "集群进行操作:delete",
            "operatorId": "62b2d434e0869c777c439867",
            "operatorName": "lhp1234",
            "status": "结束",
            "logList": null
        }
    ]
}
~~~



---

<br>


###  18 获取mongo事件日志数据数


18.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoEventLogCount/{{clusterId}}

---

18.2 请求参数：

    

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String
| eventName          |         Params           |          事件名称             |        No       |String
| status          |         Params           |         状态             |        No       |String
| operatorName          |         params           |       操作者                 |        No       |String

<br>


![img_17.png](../Images/getMongoEventLogCount.png)

----

18.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数量         |           int             |        

<br>


![img_18.png](../Images/getMongoEventLogCount_r.png)

---

<br>


###  19 查找mongoDB集群信息数据


19.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/findMongoDBClusterInfoData/{{pageIndex}}/{{pageSize}}

---

19.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| pageIndex          |         Path           |        第几页               |        Yes       |int
| pageSize          |         Path           |            每页大小            |        Yes       |int
| type          |         params           |         集群类型            |        Yes       |int
| clusterName          |         params           |      集群名称           |        No       |String
| mongoMemberName          |         params           |       mongo成员名称          |        No       |String
| fcv          |         params           |       fcv         |        No       |String

<br>


![img_19.png](../Images/findMongoDBClusterInfoData.png)

----

19.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |           int            |    
| data       |         返回数据         |            List            |        

<br>

[comment]: <> (![img_15.png]&#40;../Images/findMongoDBClusterInfoData_r.png&#41;)

~~~
{
    "code": 1000,
    "data": [
        {
            "id": "62da3b1b239d00094230b463",
            "createTime": 1658469280658,
            "updateTime": 1658469280658,
            "clusterName": "sharding",
            "type": 3,
            "mongoMember": null,
            "mongoReplica": null,
            "mongoShard": {
                "id": "62da3b1b239d00094230b463",
                "createTime": 1658469280658,
                "updateTime": 1658469280658,
                "clusterName": "sharding",
                "clusterId": "62da3b1b239d00094230b463",
                "config": {
                      ...  
                },
                "mongoS": [
                    ...
                    }
                ],
                "shardingMap": {
                    ...
                },
                "operaLog": [],
                "deleteDataAndLogAble": false,
                "authAble": false,
                "userName": "",
                "password": "",
                "authDbName": "admin",
                "status": null
            },
            "status": "正常",
            "fcv": "4.2",
            "tag": "",
            "create": true
        }
    ]
}

~~~

---

<br>


###  20 查找mongoDB集群信息数据数


20.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/findMongoDBClusterInfoCount

---

20.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| fcv          |         Params           |            fcv            |        Yes       |String
| clusterName          |         Params           |            集群名称            |        No       |String
| type          |         Params           |       集群类型             |        Yes       |int
| mongoMemberName          |         Params           |     mongo成员名称                |        No       |String

<br>


![img_20.png](../Images/findMongoDBClusterInfoCount.png)

----

20.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |           int            |    
| data       |         返回数量         |          int              |        


<br>



![img_21.png](../Images/findMongoDBClusterInfoCount_r.png)

---

<br>


###  21 获取mongo db 集合


21.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoDBCollections/{{clusterId}}

---

21.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String

<br>


![img_22.png](../Images/getMongoDBCollections.png)

----

21.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |           int            |    
| data       |         返回数据         |             List           |        

<br>


~~~
{
    "code": 1000,
    "data": [
        {
            "name": "coll",
            "type": "collection",
            "options": {},
            "info": {
                "readOnly": false,
                "uuid": {
                    "type": 4,
                    "data": "OSkYm+PbSX6DaTsGUrU4rQ=="
                }
            },
            "idIndex": {
                "v": 2,
                "key": {
                    "_id": 1
                },
                "name": "_id_",
                "ns": "cc.coll"
            },
            "storageSize": 156,
            "size": 335,
            "ns": "cc.coll"
        }
    ]
}
~~~


---

<br>


###  22 获取用户mongodb集群


22.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoDBClusterUser/{{clusterId}}

---

22.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String

<br>


![img_23.png](../Images/getMongoDBClusterUser.png)

----

22.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据         |            List            |        


<br>


~~~
{
    "code": 1000,
    "data": [
        
        {
            "_id": "admin.16581342589211",
            "userId": {
                "type": 4,
                "data": "LMMiWU2KT5GVoDCbkt3B4g=="
            },
            "user": "16581342589211",
            "db": "admin",
            "credentials": {
                "SCRAM-SHA-1": {
                    "iterationCount": 10000,
                    "salt": "EtUoKxhxaN78GCaQVKduRg==",
                    "storedKey": "pZma/HuyZVNFzSB1PU9ROxMvblc=",
                    "serverKey": "av4+YbsNnwRnb1RKeFewS5ocHIo="
                }
            },
            "authenticationRestrictions": [
                {
                    "clientSource": [
                        "192.168.3.200"
                    ]
                }
            ],
            "roles": [
                {
                    "role": "root",
                    "db": "admin"
                }
            ]
        }
        ...
    ]
}
~~~


---

<br>


###  23 获取mongodb角色数据


23.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoDBClusterRole/{{clusterId}}

---

23.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String

<br>


![img_24.png](../Images/getMongoDBClusterRole.png)

----

23.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据         |          List              |        

<br>



~~~
{
    "code": 1000,
    "data": [
        {
            "role": "__queryableBackup",
            "db": "admin",
            "isBuiltin": true,
            "roles": [],
            "inheritedRoles": [],
            "privileges": [
                {
                    "resource": {
                        "db": "config",
                        "collection": "settings"
                    },
                    "actions": [
                        "find"
                    ]
                }
            ]
        }
    }
~~~
---

<br>


###  24 执行一个计划


24.1 请求路径：

POST http://{Server-Host}:{端口}/api/server/mongo/exeExplainPlan/{{clusterId}}/{{mongoMemberId}}

---

24.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String
| mongoMemberId          |         Path           |            mongo成员id            |        Yes       |String
| document          |         Body           |       请求参数               |        Yes       |Document

<br>


![img_25.png](../Images/exeExplainPlan.png)

----

24.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |          int             |    
| data       |         返回数据         |            JSON            |        

<br>


![img_26.png](../Images/exeExplainPlan_r.png)


---

<br>


###  25 获取所有mongo配置参数.


25.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/mongo/getMongoDBProcessArgument

---

25.2 请求：



----

25.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |          int             |    
| data       |         返回数据         |         List               |        


<br>


~~~
{
    "code": 1000,
    "data": [
        {
            "id": "62d511f4defb5d5af4a04045",
            "createTime": 0,
            "updateTime": 0,
            "maxVersion": null,
            "minVersion": null,
            "name": "SYSTEM_LOG_VERBOSITY",
            "options": [
                {
                    "label": "1 (v)",
                    "value": "1"
                }
            ],
            "path": "systemLog.verbosity",
            "processTypes": "ALL",
            "shortName": "verbosity",
            "type": "INTEGER",
            "credential": false
        }

    ]
}
~~~

<br>


[comment]: <> (## MongoMember)


[comment]: <> (|       Name         |     Type             |    Description      |   )

[comment]: <> (| ------------       |----------            |---------------------|)

[comment]: <> (| memberName                 |   String             |         主机名:端口          |   )

[comment]: <> (| hostName             |   String             |         主机名     |   )

[comment]: <> (| hostId              |   Long |         主机id     |   )

[comment]: <> (| port               |   String             |         端口     |   )

[comment]: <> (| version         |   String             |         版本     |   )

[comment]: <> (| upgradeVersion           |   String             |         升降级版本     |   )

[comment]: <> (| password           |   String             |         节点密码     |   )

[comment]: <> (| authDbName           |   String             |         认证库     |   )

[comment]: <> (| currentTimeMillis           |   long             |         当前时间戳     |   )

[comment]: <> (| dataDirectory           |   String             |         数据目录     |   )

[comment]: <> (| userName             |   String             |         节点用户名     |   )

[comment]: <> (| logFile             |   String             |         日志文件     |   )

[comment]: <> (| confPath             |   String             |         配置文件路径     |   )

[comment]: <> (| deleteDataAndLogAble             |   String             |         是否强制删除     |   )

[comment]: <> (| authAble             |   String             |         是否开启认证     |   )

[comment]: <> (| runShCmd             |   String             |         执行启动命令     |   )

[comment]: <> (| type             |   enum             |         节点类型     |   )

[comment]: <> (注 type:11 单例)

[comment]: <> (*)

[comment]: <> (* <p> 普通复制集)

[comment]: <> (* 31 普通成员节点)

[comment]: <> (* 32 隐藏节点)

[comment]: <> (* 33 仲裁节点)

[comment]: <> (* 34 隐藏延迟节点)

[comment]: <> (* 35 主节点)

[comment]: <> (* <p> config复制集)

[comment]: <> (* 41 config普通成员节点)

[comment]: <> (* 42 config隐藏节点)

[comment]: <> (* 43 config仲裁节点)

[comment]: <> (* 44 config隐藏延迟节点)

[comment]: <> (* 45 config主节点)

[comment]: <> (* <p> shard复制集)

[comment]: <> (* 51 shard普通成员节点)

[comment]: <> (* 52 shard隐藏节点)

[comment]: <> (* 53 shard仲裁节点)

[comment]: <> (* 54 shard隐藏延迟节点)

[comment]: <> (* 55 shard主节点)

[comment]: <> (* <p> mongoS)

[comment]: <> (* 61 mongoS)

[comment]: <> (---)

[comment]: <> (---)
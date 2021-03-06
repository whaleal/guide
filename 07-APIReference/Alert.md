

# Alert接口
接口调用时须在请求头中设置OPS-Token,返回内容为 JSON 格式的信息.
其参数为时间类型都以时间戳形式传递。

接口调用时需用到hostId、objectId
~~~
hostId在“根据主机名模糊查询主机基本信息”接口处获取。

objectId 为主机id或mongo节点id，mongo节点id在“查找mongoDB集群信息数据”接口返回结果集中data集合的中mongo集合的“id”。
~~~



### 请求头默认格式，特殊情况特殊声明

| KEY                |     VALUE      |     
| -------------------|----------------------|
| Accept-Encoding        |         gzip, deflate, br |     
| Connection          |         keep-alive           |          
| Content-Type          |         application/json |    
---

<br>


###  1 判断来自警告信息是否正确


1.1 请求路径：

POST http://{Server-Host}:{端口}/api/alert/judgeAlertMsg


---

1.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|    alertMsgEntity   |      Body      |       告警信息实体对象     |      Yes            |    AlertMsgEntity


<br>


![img_16.png](../Images/judgeAlertMsg.png)

~~~
EX. 判断来自警告信息是否正确;其中AlertMsgEntity 如下所示：
{
	"_id" : "62b922795ba3cf1e7abf0dce",                 
	"continuousGranularityStrategyList" : [ ],
	"createTime" : "1656300153918",
	"objectId" : "62b922795ba3cf1e7abf0dcd",
	"timeFrequencyStrategyList" : [ ],
	"type" : 1,                                             
	"updateTime" : "1656300153918"
}
~~~


----

1.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |           int            |    
| data       |         返回信息        |                String         | 

<br>



![img_17.png](../Images/judgeAlertMsg_r.png)




---

<br>

###  2 获取告警策略


2.1 请求路径：

GET http://{Server-Host}:{端口}/api/alert/getAlertStrategy


---

2.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|     objectId        |        Params              |           对象id               |    Yes              |String
|     type        |         Params       |    类型:1 agent,2 mongo    |           Yes       |String

<br>


![img_18.png](../Images/getAlertStrategy.png)

----

2.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |    
| data       |         返回数据        |             List            | 

<br>



![img_19.png](../Images/getAlertStrategy_r.png)



---

<br>

###  3 获取所有成员警告策略


3.1 请求路径：

GET http://{Server-Host}:{端口}/api/alert/getAllMongoMemberAlertStrategy


---

3.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|     hostId        |        Params              |           主机id               |    Yes              |String

<br>


![img_20.png](../Images/getAllMongoMemberAlertStrategy.png)

----

3.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据        |           List              | 


<br>


![img_21.png](../Images/getAllMongoMemberAlertStrategy_r.png)



---

<br>

###  4 更新警告信息


4.1 请求路径：

POST http://{Server-Host}:{端口}/api/alert/update


---

4.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|     alertStrategyEntity        |        Body              |           告警策略实体对象              |    Yes              |alertStrategyEntity

<br>


![img_22.png](../Images/alert_update.png)

----

4.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据        |              String           | 

<br>



![img_23.png](../Images/alert_update_r.png)


---

<br>


[comment]: <> (## AlertStrategyEntity)


[comment]: <> (|       Name         |     Type             |    Description      |   )

[comment]: <> (| ------------       |----------            |---------------------|)

[comment]: <> (| name                 |   String             |         主机或mongoMember警告策略名称          |   )

[comment]: <> (| objectId             |   String             |         主机id or mongoMemberId     |   )

[comment]: <> (| type                 |   String |         1 agent 2 mongo     |   )

[comment]: <> (| timeFrequencyStrategyList         |   List\<TimeFrequencyStrategy>             |         时间区间警告策略     |   )

[comment]: <> (| continuousGranularityStrategyList         |      List\<ContinuousGranularityStrategy>          |         连续时间警告策略     |   )


[comment]: <> (---)

[comment]: <> (---)

[comment]: <> (## TimeFrequencyStrategy)


[comment]: <> (|       Name         |     Type             |    Description      |   )

[comment]: <> (| ------------       |----------            |---------------------|)

[comment]: <> (| startHour                 |   int             |         小时时间范围的起点          |   )

[comment]: <> (| endHour             |   int            |         小时时间范围的结点     |   )


[comment]: <> (---)

[comment]: <> (---)

[comment]: <> (## HostInfoMongoEntity)


[comment]: <> (|       Name         |     Type             |    Description      |   )

[comment]: <> (| ------------       |----------            |---------------------|)

[comment]: <> (| duration                 |   int             |         统计颗粒度          |   )


[comment]: <> (---)

[comment]: <> (---)

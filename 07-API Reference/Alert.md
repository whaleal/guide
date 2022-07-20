

# Alert接口
此接口调用时须在请求头中设置OPS-Token ，填写参数发起请求，返回内容为 JSON 格式的信息。



### 请求头默认格式，特殊情况特殊声明

| KEY                |     VALUE      |     
| -------------------|----------------------|
| Accept-Encoding        |         gzip, deflate, br |     
| Connection          |         keep-alive           |          
| Content-Type          |         application/json |    
---




####  1 判断来自警告信息是否正确


1.1 请求路径：

POST http://192.168.3.200:9600/api/alert/judgeAlertMsg


---

1.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|    AlertMsgEntity   |      body      |       告警信息实体类      |      yes            |    AlertMsgEntity

![img_16.png](../Images/judgeAlertMsg.png)

----

1.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回信息        |                         | 


![img_17.png](../Images/judgeAlertMsg_r.png)





---
---


####  2 获取告警策略


2.1 请求路径：

GET http://192.168.3.200:9600/api/alert/getAlertStrategy


---

2.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|     objectId        |        params              |           对象id               |    yes              |string
|     type        |         params             |            类型              |           yes       |string

![img_18.png](../Images/getAlertStrategy.png)

----

2.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据        |                         | 


![img_19.png](../Images/getAlertStrategy_r.png)


---
---


####  3 获取所有成员警告策略


3.1 请求路径：

GET http://192.168.3.200:9600/api/alert/getAllMongoMemberAlertStrategy


---

3.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|     hostId        |        params              |           主机id               |    yes              |string

![img_20.png](../Images/getAllMongoMemberAlertStrategy.png)

----

3.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据        |                         | 


![img_21.png](../Images/getAllMongoMemberAlertStrategy_r.png)


---
---


####  4 更新警告信息


4.1 请求路径：

POST http://192.168.3.200:9600/api/alert/update


---

4.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|     alertStrategyEntity        |        body              |           告警策略实体类               |    yes              |alertStrategyEntity

![img_22.png](../Images/alert_update.png)

----

4.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据        |                         | 


![img_23.png](../Images/alert_update_r.png)


---
---

---  

## AlertStrategyEntity


|       Name         |     Type             |    Description      |   
| ------------       |----------            |---------------------|
| name                 |   string             |         主机或mongoMember警告策略名称          |   
| objectId             |   string             |         主机id or mongoMemberId     |   
| type                 |   string |         1 agent 2 mongo     |   
| timeFrequencyStrategyList         |   List\<TimeFrequencyStrategy>             |         时间区间警告策略     |   
| continuousGranularityStrategyList         |      List\<ContinuousGranularityStrategy>          |         连续时间警告策略     |   


---
---

## TimeFrequencyStrategy


|       Name         |     Type             |    Description      |   
| ------------       |----------            |---------------------|
| startHour                 |   int             |         小时时间范围的起点          |   
| endHour             |   int            |         小时时间范围的结点     |   


---
---

## HostInfoMongoEntity


|       Name         |     Type             |    Description      |   
| ------------       |----------            |---------------------|
| duration                 |   int             |         统计颗粒度          |   


---
---
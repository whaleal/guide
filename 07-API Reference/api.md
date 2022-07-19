



#1、Agent接口
此接口调用时须在请求头中设置OPS-Token ，填写参数发起请求，返回内容为 JSON 格式的信息。


---


 #### 1 根据主机名模糊查询主机基本信息（主机名和主机ID）



1.1 请求路径：


Get : http://192.168.3.200:9600/api/server/agent/getAllAgentHostNameAndHostId

---
1.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| hostName          |         参数           |            主机名称            |        No       |string        |


![img.png](https://github.com/whaleal/guide/blob/main/Images/img.png)

----

1.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据         |                        |        

![img_1.png](https://github.com/whaleal/guide/blob/main/Images/img_1.png)

---



####2. 获取Agent的统计信息


2.1 请求路径：

Get : http://192.168.3.200:9600/api/server/agent/getAgentStatistics


2.2 请求参数：




| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|       |                    |                        |               |        |


![img_2.png](https://github.com/whaleal/guide/blob/main/Images/img_2.png)


2.3 返回结果:


|               |     Description    |           Schema              |  
| -------------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |            long           |    
| data.activeAgentNum    |         Agent存活数         |            long            |    
| data.activeAgentCpuNum     |         Agent CPU存活数         |            long            |    
| data.activeAgentDiskNum     |         Agent 磁盘存活数         |            long            |    
| data.deadAgentMemoryNum     |         Agent 内存死亡数         |            long            |    
| data.deadAgentCpuNum     |         Agent CPU死亡数         |            long            |    
| data.activeAgentMemoryNum    |         Agent 内存存活数         |            long            |    
| data.deadAgentNum     |         Agent 死亡数         |            long            |    
| data.deadAgentDiskNum    |         Agent 磁盘死亡数         |            long            |    


![img_3.png](https://github.com/whaleal/guide/blob/main/Images/img_3.png)

#### 3.获取所有主机信息



3.1 请求路径：

GET  http://192.168.3.200:9600/api/server/agent/getAllAgentData/{{pageIndex}}/{{pageSize}}

---
1.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| pageIndex          |         path           |            第几页           |        yes       |int        |
| pageSize          |         path         |            每页大小            |        yes      |int        |
| hostName          |         参数           |            主机名称            |        No       |string        |
| Ip          |         参数           |            主机ip            |        No       |string        |
| Status          |         参数           |            主机状态            |        No       |Boolean        |


![img_4.png](https://github.com/whaleal/guide/blob/main/Images/img_4.png)

----

3.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据         |            List\<HostInfoMongoEntity>            |        

{"code":1000,"data":[{"id":"62b153a344ba1b7771c42df7","createTime":1657077138160,"updateTime":1657096989910,"hostId":"62b153a344ba1b7771c42df7","hostName":"server100","hostNameLong":"server100","ipInfo":[{"ip":"192.168.3.100","type":"ipv4"},{"ip":"192.168.3.100","type":"外部ip"}],"memory":128722,"osVersion":"CentOS Linux release 7.9.2009 (Core)","cpuInfo":" Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz","cpuNum":40,"swap":4095,"kernelInfo":"3.10.0-1160.24.1.el7.x86_64","totalDiskSize":7893956,"run":true,"systemPropertyInfo":{"javaVersion":"11.0.9","javaVendor":"Oracle Corporation","javaVendorUrl":null,"javaHome":"/root/jdk-11.0.9","javaVmSpecificationVersion":"11","javaVmSpecificationVendor":null,"javaVmSpecificationName":"Java Virtual Machine Specification","javaVmVersion":"11.0.9+7-LTS","javaVmVendor":"Oracle Corporation","javaVmName":"Java HotSpot(TM) 64-Bit Server VM","javaSpecificationVersion":null,"javaSpecificationVendor":"Oracle Corporation","javaSpecificationName":"Java Platform API Specification","javaClassVersion":"55.0","javaClassPath":"agent-collection-1.0.0.jar","javaLibraryPath":"/usr/java/packages/lib:/usr/lib64:/lib64:/lib:/usr/lib","javaIoTmpdir":"/tmp","javaCompiler":null,"javaExtDirs":null,"fileSeparator":"/","pathSeparator":":","lineSeparator":"\n","userName":"root","userHome":"/root","userDir":"/home/jmops","osversion":"3.10.0-1160.24.1.el7.x86_64","osname":"Linux","osarch":"amd64"}}]}

---

#### 4.获取所有主机count


4.1 请求路径：


GET http://192.168.3.200:9600/api/server/agent/getAllAgentCount

---


4.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| hostName          |         参数           |            主机名称            |        No       |string        |
| ip          |         参数           |            主机ip            |        No       |string        |
| status          |         参数           |            主机状态            |        No       |Boolean        |


![img_5.png](https://github.com/whaleal/guide/blob/main/Images/img_5.png)

----

4.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                      |    
| data       |         返回数量         |                       |        

![img_6.png](https://github.com/whaleal/guide/blob/main/Images/img_6.png)

---

#### 5.获取某主机静态信息


5.1 请求路径：

GET http://192.168.3.200:9600/api/server/agent/getAgentInfo/{{hostId}}

---
5.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| hostId         |         path           |            主机id           |        yes       |string        |


![img_7.png](https://github.com/whaleal/guide/blob/main/Images/img_7.png)

----

5.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                         |    
| data       |         返回数据         |            HostInfoMongoEntity            |        

{"code":1000,"data":{"id":"62bbfbe9a46517610435d615","createTime":1657077194390,"updateTime":1657097252146,"hostId":"62bbfbe9a46517610435d615","hostName":"chen","hostNameLong":"chen","ipInfo":[{"ip":"192.168.3.80","type":"ipv4"},{"ip":"192.168.3.80","type":"外部ip"}],"memory":7821,"osVersion":"CentOS Linux release 7.7.1908 (Core)","cpuInfo":" Intel(R) Xeon(R) CPU L5640 @ 2.27GHz","cpuNum":4,"swap":8063,"kernelInfo":"3.10.0-1062.el7.x86_64","totalDiskSize":213035,"run":true,"systemPropertyInfo":{"javaVersion":"1.8.0_172","javaVendor":"Oracle Corporation","javaVendorUrl":null,"javaHome":"/home/docker20220629BAK/java/jre","javaVmSpecificationVersion":"1.8","javaVmSpecificationVendor":null,"javaVmSpecificationName":"Java Virtual Machine Specification","javaVmVersion":"25.172-b11","javaVmVendor":"Oracle Corporation","javaVmName":"Java HotSpot(TM) 64-Bit Server VM","javaSpecificationVersion":null,"javaSpecificationVendor":"Oracle Corporation","javaSpecificationName":"Java Platform API Specification","javaClassVersion":"52.0","javaClassPath":"agent-collection-1.0.0.jar","javaLibraryPath":"/usr/java/packages/lib/amd64:/usr/lib64:/lib64:/lib:/usr/lib","javaIoTmpdir":"/tmp","javaCompiler":null,"javaExtDirs":"/home/docker20220629BAK/java/jre/lib/ext:/usr/java/packages/lib/ext","fileSeparator":"/","pathSeparator":":","lineSeparator":"\n","userName":"root","userHome":"/root","userDir":"/home","osversion":"3.10.0-1062.el7.x86_64","osname":"Linux","osarch":"amd64"}}}


---

#### 6.获取agent的监控信息



6.1 请求路径：

GET http://192.168.3.200:9600/api/server/agent/getAgentMonitor/map/{{hostId}}/{{type}}

---

6.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| hostId         |         path           |            主机id            |        yes       |string        |
| type         |         path           |            监控类型            |        yes       |string        |
| startTimeForTimeInterval         |         参数           |      某时间段的开始时间            |        yes       |long        |
| endTimeForTimeInterval         |         参数           |            某时间段的结束时间    |        yes       |long        |
| timeGranularity         |         参数           |            时间粒度            |        yes       |long        |


![img_8.png](https://github.com/whaleal/guide/blob/main/Images/img_8.png)

----

6.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                      |    
| data       |         返回数据         |        Map<String,Object>                |        

{"code":1000,"data":{"内存/GB":{"cache":[24.85,36.33,37.58,43.05,49.25,48.12,47.66,46.84],"name":"memory","used":[67.82,69.8,73.28,72.63,75.38,76.37,76.82,77.43],"free":[33.03,19.57,14.85,10.02,1.08,1.21,1.22,1.43],"message":{"free":"空闲内存 单位MB","used":"已使用内存 单位MB","cache":"缓存内存 单位MB","ava":"可用内存 单位MB"},"ava":[57.27,55.3,51.81,52.46,49.71,48.72,48.27,47.66]},"cpu/%":{"sy":[0.48,0.58,0.64,0.83,0.96,1.11,1.24,1.38],"name":"cpu","id":[98.95,98.69,98.54,97.8,97.38,97.1,96.86,96.52],"message":{"id":"cpu空闲率 单位百分比%","us":"cpu用户使用率 单位百分比%","sy":"cpu系统使用率 单位百分比%"},"us":[0.57,0.72,0.79,1.3,1.53,1.73,1.83,2.02]},"net/KB":{"data":{"lo":{"in":[2196.86,2279.41,3231.01,8018.15,9043.2,9681.84,12201.41,14372.73],"name":"lo","out":[2196.99,2280.6,3231.44,8018.37,9044.2,9682.23,12201.73,14373.14]},"em1":{"in":[656.26,876.46,820.59,1801.78,1622.69,661.78,630.79,647.14],"name":"em1","out":[656.31,876.51,820.61,1801.78,1622.71,661.8,630.8,647.15]},"em3":{"in":[0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0],"name":"em3","out":[0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0]},"em2":{"in":[0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0],"name":"em2","out":[0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0]},"em4":{"in":[0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0],"name":"em4","out":[0.0,0.0,0.0,0.0,0.0,0.0,0.0,0.0]}},"name":"net","message":{"in":"流入流量 单位KB/S","out":"流出流量 单位KB/S"}},"diskIO/KB":{"data":{"dm-2":{"util":[0.6,0.59,0.59,0.59,0.59,0.59,0.58,0.58],"name":"dm-2","rkB":[2.23,2.16,2.13,2.13,2.42,2.56,2.68,2.8],"wkB":[49309.07,7023.58,47269.53,47155.17,53426.61,56430.74,59026.42,61681.28]},"sda":{"util":[0.83,0.82,0.81,0.81,0.83,0.83,0.82,0.81],"name":"sda","rkB":[3.89,4.12,4.06,4.16,10.6,10.6,10.56,10.51],"wkB":[85412.74,12577.95,89132.09,91171.64,230346.14,230303.49,229439.3,228407.05]},"dm-1":{"util":[0.0,0.0,0.0,0.0,0.01,0.01,0.01,0.01],"name":"dm-1","rkB":[0.04,0.04,0.04,0.14,0.46,0.45,0.44,0.44],"wkB":[864.14,108.21,864.13,2935.93,9938.06,9780.45,9604.71,9433.55]},"dm-0":{"util":[0.26,0.26,0.26,0.25,0.27,0.27,0.26,0.26],"name":"dm-0","rkB":[1.6,1.9,1.87,1.88,7.7,7.57,7.42,7.25],"wkB":[34892.1,5451.67,40710.06,40798.14,166637.73,163782.31,160518.73,157011.22]}},"name":"diskIO","message":{"util":"使用率 单位百分比","rkB":"读 单位KB/S","wkB":"写 单位KB/S"}}},"size":8,"createTime":[1656504001000,1656584997000,1656590401000,1656633601000,1656676801000,1656720001000,1656763201000,1656806401000]}


---


#### 7.获取agent的日志信息，结果分页展示



7.1 请求路径：


GET http://192.168.3.200:9600/api/server/agent/logData/{{hostId}}/{{pageIndex}}/{{pageSize}}

---

7.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| hostid          |         path           |            主机id           |        yes       |string        |
| pageIndex          |         path           |            第几页            |        yes       |Integer        |
| pageSize          |         path           |            每页数量            |        yes       |Integer        |
| type          |         参数           |            日志类别            |        No       |string        |
| startTime          |         参数           |            开始时间            |        yes       |long        |
| endTime          |         参数           |            结束时间            |        yes       |long        |
| content          |         参数           |            关键字            |        No       |string        |


![img_9.png](https://github.com/whaleal/guide/blob/main/Images/img_9.png)

----

7.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据         |     AgentLogEntity         |       


![img_10.png](https://github.com/whaleal/guide/blob/main/Images/img_10.png)


---


#### 8.获取agent的日志信息数量



8.1 请求路径：


GET http://192.168.3.200:9600/api/server/agent/logCount/{{hostId}}

---

8.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| hostid          |         path           |            主机id           |        yes       |string        |
| type          |         参数           |            日志类别            |        No       |string        |
| startTime          |         参数           |            开始时间            |        yes       |long        |
| endTime          |         参数           |            结束时间            |        yes       |long        |
| content          |         参数           |            关键字            |        No       |string        |


![img_11.png](https://github.com/whaleal/guide/blob/main/Images/img_11.png)

----

8.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数量        |                        |       



![img_12.png](https://github.com/whaleal/guide/blob/main/Images/img_12.png)


---

#### 9.操作agent的命令



9.1 请求路径：


GET http://192.168.3.200:9600/api/server/agent/operate/{{hostId}}/{{operateType}}

---

9.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| hostId          |         path           |            主机id            |        yes       |string        |
| operateType          |         path           |   操作类别:mongo,host      |        yes       |string        |


![img_13.png](https://github.com/whaleal/guide/blob/main/Images/img_13.png)

----

9.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| msg       |         返回消息         |            string            |       

![img_14.png](https://github.com/whaleal/guide/blob/main/Images/img_14.png)


#### 10.生成agentId


10.1 请求路径：

GET http://192.168.3.200:9600/api/server/agent/generateAgentId


---


10.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|           |                     |                        |               |        |


![img_15.png](https://github.com/whaleal/guide/blob/main/Images/img_15.png)

----

10.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         agentid         |       string                 |        

![img_16.png](https://github.com/whaleal/guide/blob/main/Images/img_16.png)

---




#### 11.下载agentFile



11.1 请求路径：

GET http://192.168.3.200:9600/api/server/agent/downAgentFile/{{agentId}}/agent-collection-1.0.0.jar

---

11.2 请求参数：



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| agentId          |         Path           |            agentId            |        Yes       |string        |


![img_17.png](https://github.com/whaleal/guide/blob/main/Images/img_17.png)

----

11.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| File       |         二进制流形式返回文件         |       File                 |        


---


#### 12.获取agent执行命令记录

12.1 请求路径：

GET http://192.168.3.200:9600/api/server/agent/getExecCommandDataList/{{hostId}}/{{pageIndex}}/{{pageSize}}

---

12.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| hostId          |         Path           |            主机名称            |        Yes       |string        |
| pageIndex          |         Path           |            分页页数            |        Yes       |Integer        |
| pageSize          |         Path           |            分页大小            |        Yes       |Integer        |
| Status          |         参数           |            状态            |        No       |Int        |
| startTime          |         参数           |            开始时间            |        Yes       |Long        |
| endTime          |         参数           |            结束时间            |        Yes       |Long        |
| commandType          |         参数           |            命令类型            |        No       |string        |
| result          |         参数           |            结果            |        No       |string        |
| eventId          |         参数           |            事件id            |        No       |string        |


![img_18.png](https://github.com/whaleal/guide/blob/main/Images/img_18.png)

----

12.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据         |             List\<CommandEntity>            |        

![img_19.png](https://github.com/whaleal/guide/blob/main/Images/img_19.png)

---


#### 13.获取agent执行命令记录数

13.1 请求路径：

GET http://192.168.3.200:9600/api/server/agent/getExecCommandDataCount/{{hostId}}

---

13.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| hostId          |         Path           |            主机名称            |        Yes       |string        |
| Status          |         参数           |            状态            |        No       |int|
| startTime          |         参数           |            开始时间            |        Yes       |Long        |
| endTime          |         参数           |            结束时间            |        Yes       |Long        |
| commandType          |         参数           |            命令类型            |        No       |string        |
| result          |         参数           |            结果            |        No       |string        |
| eventId          |         参数           |            时间id            |        No       |string        |


![img_20.png](https://github.com/whaleal/guide/blob/main/Images/img_20.png)

----

13.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数数量         |            long            |        


![img_21.png](https://github.com/whaleal/guide/blob/main/Images/img_21.png)


---



####  14.获取主机cpu使用率前五


14.1 请求路径：

GET http://192.168.3.200:9600/api/server/agent/getHost/CpuUsage/top/five

---

14.2 请求参数：

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| beginTime          |         参数           |            开始时间            |        Yes       |Long        |
| endTime          |         参数           |            结束时间            |        Yes       |Long        |


![img_22.png](https://github.com/whaleal/guide/blob/main/Images/img_22.png)

----

14.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data.[index].host       |         主机id         |         String               |        
| data.[index].hostName       |         主机名称         |         String               |        
| data.[index].usage       |         使用率         |         Double               |        


![img_23.png](https://github.com/whaleal/guide/blob/main/Images/img_23.png)

---



####  15.获取主机内存使用率前五

15.1 请求路径：

GET http://192.168.3.200:9600/api/server/agent/getHost/MemUsage/top/five

---

15.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| beginTime          |         参数           |            开始时间            |        Yes       |Long        |
| endTime          |         参数           |            结束时间            |        Yes       |Long        |


![img_24.png](https://github.com/whaleal/guide/blob/main/Images/img_24.png)

----

15.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data.[index].host       |         主机id         |         String               |        
| data.[index].hostName       |         主机名称         |         String               |        
| data.[index].usage       |         使用率         |         Double               |      

![img_25.png](https://github.com/whaleal/guide/blob/main/Images/img_25.png)

---



#### 16.获取主机磁盘使用率前五


16.1 请求路径：

GET http://192.168.3.200:9600/api/server/agent/getHost/DiskUsage/top/five

---

16.2 请求参数：

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| beginTime          |         参数           |            开始时间            |        Yes       |Long        |
| endTime          |         参数           |            结束时间            |        Yes       |Long        |


![img_26.png](https://github.com/whaleal/guide/blob/main/Images/img_26.png)

----

16.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data.[index].host       |         主机id         |         String               |        
| data.[index].hostName       |         主机名称         |         String               |        
| data.[index].usage       |         使用率         |         Double               |  

![img_27.png](https://github.com/whaleal/guide/blob/main/Images/img_27.png)

---



####  17.获取网卡输入使用率前五


17.1 请求路径：


GET http://192.168.3.200:9600/api/server/agent/getHost/NetIn/top/five

---

17.2 请求参数：

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| beginTime          |         参数           |            开始时间            |        Yes       |Long        |
| endTime          |         参数           |            结束时间            |        Yes       |Long        |


![img_28.png](https://github.com/whaleal/guide/blob/main/Images/img_28.png)

----

17.3 返回结果

|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data.[index].host       |         主机id         |         String               |        
| data.[index].hostName       |         主机名称         |         String               |        
| data.[index].usage       |         使用率         |         Double               |  


![img_29.png](https://github.com/whaleal/guide/blob/main/Images/img_29.png)

---



####  18.获取网卡输出使用率前五

18.1 请求路径：

GET http://192.168.3.200:9600/api/server/agent/getHost/NetOut/top/five

---

18.2 请求参数：

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| beginTime          |         参数           |            开始时间            |        Yes       |Long        |
| endTime          |         参数           |            结束时间            |        Yes       |Long        |


![img_30.png](https://github.com/whaleal/guide/blob/main/Images/img_30.png)

----

18.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data.[index].host       |         主机id         |         String               |        
| data.[index].hostName       |         主机名称         |         String               |        
| data.[index].usage       |         使用率         |         Double               |  

![img_31.png](https://github.com/whaleal/guide/blob/main/Images/img_31.png)

---
---

##Info


|       Name        |     Type    |           Description       |   
| --------------|----------------------|--------------------|
| id        |   string |         Id              |   
| name        |   string |         主机名称              |   


___

##ipInfo

|       Name        |     Type    |           Description       |   
| --------------|----------------------|--------------------|
| id        |   string |         Id              |   
| Type        |   string |         主机名称              |   


---  

##HostInfoMongoEntity


|       Name         |     Type             |    Description      |   
| ------------       |----------            |---------------------|
| id                 |   string             |         Id          |   
| ipInfo             |   List<ipInfo>             |         Ip信息     |   
| systemPropertyInfo |   systemPropertyInfo |         系统参数信息     |   
| createTime         |   时间戳             |         创建时间     |   
| updateTime         |   时间戳             |         更新时间     |   
| hostName           |   string             |         主机名称     |   
| hostId             |   string             |         主机id     |   
| hostNameLong       |   string             |         主机长名称     |   
| Memory             |   int             |         内存     |   
| osVersion          |   string             |         系统版本     |   
| cpuNum             |   int             |         Cpu数     |   
| swap               |   int             |         交换内存     |   
| kernelInfo         |   string             |         内核信息     |   
| totalDiskSize      |   Int             |         总磁盘大小     |   
| run                |   Boolean             |         是否正在运行     |   



---
---













#2、File接口
此接口调用时须在请求头中设置OPS-Token ，填写参数发起请求，返回内容为 JSON 格式的信息。


---


####  1 上传文件到Server端


1.1 请求路径：

POST http://192.168.3.200:9600/api/server/file/web/upload/file

---

1.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| File          |         formData           |            上传的文件            |        Yes       |MultipartFile


![img_32.png](https://github.com/whaleal/guide/blob/main/Images/img_32.png)

----

1.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| msg       |         消息         |                        |        

![img_33.png](https://github.com/whaleal/guide/blob/main/Images/img_33.png)

---



####  2 删除server端文件



2.1 请求路径：

GET http://192.168.3.200:9600/api/server/file/deleteFile/{{filename}}

---

2.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| filename          |         Path           |            文件名称            |        Yes       |String        |


![img_34.png](https://github.com/whaleal/guide/blob/main/Images/img_34.png)

----

2.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| msg       |         返回消息         |                        |        


![img_35.png](https://github.com/whaleal/guide/blob/main/Images/img_35.png)

---



#### 3 获取server端的文件信息.



3.1 请求路径：

GET http://192.168.3.200:9600/api/server/file/getAllMongoFile

---

3.2 请求参数：

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
|            |                     |                         |                |         |


![img_36.png](https://github.com/whaleal/guide/blob/main/Images/img_36.png)

----

3.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据         |        MongoFile                |        

![img_37.png](https://github.com/whaleal/guide/blob/main/Images/img_37.png)

---



---
---


##MongoFile


|       Name         |     Type             |    Description      |   
| ------------       |----------            |---------------------|
| shortName                 |   string             |         姓          |   
| Name             |   string             |         名     |   
| Size              |   Long |         大小     |   
| Md5               |   string             |         文件校验     |   
| version         |   string             |         版本     |   
| path           |   string             |         路径     |   
| hostId             |   string             |         主机id     |   


---
---



#3、Member接口
此接口调用时须在请求头中设置OPS-Token ，填写参数发起请求，返回内容为 JSON 格式的信息。


---


####  1 登录

1.1 请求路径：


POST http://192.168.3.200:9600/api/server/member/login

---

1.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| account          |         formData           |            账户名            |        Yes       |String        |
| password          |         formData           |            密码            |        Yes       |String        |


![img_38.png](https://github.com/whaleal/guide/blob/main/Images/img_38.png)

----

2.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据|       MemberMongoEntity                 |        
| generateAgentIdAble       |         是否有权限生成agentid         |         Boolean               |        
| token       |         Token令牌         |                        |        String

![img_39.png](https://github.com/whaleal/guide/blob/main/Images/img_39.png)


---


#### 2 保存新用户信息.

2.1 请求路径：


POST http://192.168.3.200:9600/api/server/member/register

---

2.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| account          |         formData           |            账户名            |        Yes       |String        |
| password          |         formData           |            密码            |        Yes       |String        |
| email          |         formData           |            邮箱            |        Yes       |String        |
| phone          |         formData           |            手机号            |        Yes       |String        |


![img_40.png](https://github.com/whaleal/guide/blob/main/Images/img_40.png)

----

2.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据|       MemberMongoEntity                 |        



![img_41.png](https://github.com/whaleal/guide/blob/main/Images/img_41.png)



---


####  3 更新用户信息


3.1 请求路径：


POST http://192.168.3.200:9600/api/server/member/update

---

3.2 请求参数：



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| account          |         formData           |            账户名            |        Yes       |String        |
| password          |         formData           |            密码            |        Yes       |String        |
| email          |         formData           |            邮箱            |        Yes       |String        |
| phone          |         formData           |            手机号            |        Yes       |String        |
| Id          |         formData           |            Id            |        Yes       |String        |


![img_42.png](https://github.com/whaleal/guide/blob/main/Images/img_42.png)

----

3.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据|       MemberMongoEntity                 |        

![img_43.png](https://github.com/whaleal/guide/blob/main/Images/img_43.png)

---


#### 4 搜索用户

4.1 请求路径：


POST http://192.168.3.200:9600/api/server/member/findMemberData/{{pageSize}}/{{pageIndex}}

---

4.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| pageSize          |         path           |            每页大小            |        Yes       |int        |
| pageIndex          |         path           |            第几页            |        Yes       |int        |
| account          |         formData           |            账户名            |        Yes       |String        |
| password          |         formData           |            密码            |        Yes       |String        |
| email          |         formData           |            邮箱            |        Yes       |String        |
| phone          |         formData           |            手机号            |        Yes       |String        |

![img_44.png](https://github.com/whaleal/guide/blob/main/Images/img_44.png)

----

4.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数据|       MemberMongoEntity                 |        


![img_45.png](https://github.com/whaleal/guide/blob/main/Images/img_45.png)


---


#### 5 查询用户数量

5.1 请求路径：

POST http://192.168.3.200:9600/api/server/member/findMemberCount

---

5.2 请求参数：



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| account          |         formData           |            账户名            |        Yes       |String        |
| password          |         formData           |            密码            |        Yes       |String        |
| email          |         formData           |            邮箱            |        Yes       |String        |
| phone          |         formData           |            手机号            |        Yes       |String        |

![img_46.png](https://github.com/whaleal/guide/blob/main/Images/img_46.png)

----

5.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| data       |         返回数量         |                        |        

![img_47.png](https://github.com/whaleal/guide/blob/main/Images/img_47.png)

---


#### 6 更新接收警报

6.1 请求路径：


GET http://192.168.3.200:9600/api/server/member/update/receiveAlert/{{memberId}}/{{value}}

---

6.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| value          |         Path           |            是否开启            |        Yes       |Boolean        |


![img_48.png](https://github.com/whaleal/guide/blob/main/Images/img_48.png)

----

6.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| msg       |         返回消息|                        |        

![img_49.png](https://github.com/whaleal/guide/blob/main/Images/img_49.png)

---


#### 7 更新时区

7.1 请求路径：


GET http://192.168.3.200:9600/api/server/member/update/timezone/{{memberId}}

---

7.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| timezone          |         参数           |            时区            |        Yes       |String        |

![img_50.png](https://github.com/whaleal/guide/blob/main/Images/img_50.png)

----

7.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| msg       |         返回消息|                        |        

![img_51.png](https://github.com/whaleal/guide/blob/main/Images/img_51.png)



---


#### 8 更新角色


8.1 请求路径：


GET http://192.168.3.200:9600/api/server/member/update/role/{{memberId}}/{{value}}

---

8.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| value          |         Path           |            角色:user,admin            |        Yes       |String        |

![img_52.png](https://github.com/whaleal/guide/blob/main/Images/img_52.png)

----

8.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| msg       |         返回消息|                        |    

![img_53.png](https://github.com/whaleal/guide/blob/main/Images/img_53.png)

---


#### 9 更新是否可以创建mongodb

9.1 请求路径：

GET http://192.168.3.200:9600/api/server/member/update/createMongoDBAble/{{memberId}}/{{value}}

---

9.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| value          |         Path           |            是否开启            |        Yes       |Boolean        |

![img_54.png](https://github.com/whaleal/guide/blob/main/Images/img_54.png)

----

9.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| msg       |         返回消息|                        |    

![img_55.png](https://github.com/whaleal/guide/blob/main/Images/img_55.png)


---


#### 10 更新是否可以创建agenid

10.1 请求路径：

GET http://192.168.3.200:9600/api/server/member/update/generateAgentIdAble/{{memberId}}/{{value}}

---

10.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| value          |         Path           |            是否开启            |        Yes       |Boolean        |

![img_56.png](https://github.com/whaleal/guide/blob/main/Images/img_56.png)

----

10.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |    
| msg       |         返回消息|                        |    


![img_57.png](https://github.com/whaleal/guide/blob/main/Images/img_57.png)



---


#### 11 更新用户资源信息

11.1 请求路径：

GET http://192.168.3.200:9600/api/server/member/update/userResourceInfo/{{memberId}}/{{objectId}}/{{type}}/{{value}}

---

11.2 请求参数：

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| value          |         Path           |            值：read，write，nul            |        Yes       |String        |
| objectId          |         Path           |            根据type类型提供id            |        Yes       |String        |
| type          |         Path           |            类型：mongo,host            |        Yes       |String        |

![img_58.png](https://github.com/whaleal/guide/blob/main/Images/img_58.png)

----

11.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |
| msg       |         返回消息|                        |

![img_59.png](https://github.com/whaleal/guide/blob/main/Images/img_59.png)

---


#### 12 删除用户

12.1 请求路径：


GET http://170.187.230.78:9602/api/server/member/delete/user/{{memberId}}

---

12.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |



![img_60.png](https://github.com/whaleal/guide/blob/main/Images/img_60.png)

----

12.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |
| msg       |         返回消息|                        |

![img_61.png](https://github.com/whaleal/guide/blob/main/Images/img_61.png)

---


#### 13 获取用户资源

13.1 请求路径：


GET http://170.187.230.78:9600/api/server/member/getUserResource/{{memberId}}

---

13.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |

![img_62.png](https://github.com/whaleal/guide/blob/main/Images/img_62.png)

----

13.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |
| data       |         返回数据|                   MemberMongoEntity     |

![img_63.png](https://github.com/whaleal/guide/blob/main/Images/img_63.png)

---


#### 14 获取用户服务数据

14.1 请求路径：


GET https://170.187.230.78:9600/api/server/member/getUserServerResourceData/{{memberId}}/{{competence}}/{{pageSize}}/{{pageIndex}}

---

14.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| competence          |         Path           |            权限:write,read,null            |        Yes       |String        |
| pageSize          |         Path           |            每页大小            |        Yes       |Int        |
| pageIndex          |         Path           |            第几页            |        Yes       |Int        |

![img_64.png](https://github.com/whaleal/guide/blob/main/Images/img_64.png)

----

14.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |
| data.hostName       |         主机名称|            String            |
| data.osVersion       |         系统版本|         String               |

![img_65.png](https://github.com/whaleal/guide/blob/main/Images/img_65.png)



---


#### 15 获取用户服务数

15.1 请求路径：

GET http://170.187.230.78:9600/api/server/member/getUserServerResourceCount/{{memberId}}/{{competence}}

---

15.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| competence          |         Path           |            权限:write,read,null            |        Yes       |String        |


![img_66.png](https://github.com/whaleal/guide/blob/main/Images/img_66.png)

----

15.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |
| data       |         返回数量|                        |

![img_67.png](https://github.com/whaleal/guide/blob/main/Images/img_67.png)

---


#### 16 获取用户mongo db集群资源数据

16.1 请求路径：


GET http://170.187.230.78:9600/api/server/member/getUserMongoDBClusterResourceData/{{memberId}}/{{competence}}/{{pageSize}}/{{pageIndex}}

---

16.2 请求参数：

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| competence          |         Path           |            权限:write,read,null            |        Yes       |String        |
| pageSize          |         Path           |            每页大小            |        Yes       |Int        |
| pageIndex          |         Path           |            第几页            |        Yes       |Int        |



![img_68.png](https://github.com/whaleal/guide/blob/main/Images/img_68.png)

----

16.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |
| data.clusterName       |         集群名称|                        |
| data.type       |         类型:单节点,复制集,分片，纳管|                        |


![img_69.png](https://github.com/whaleal/guide/blob/main/Images/img_69.png)

---


#### 17 获取用户mongo db集群数

17.1 请求路径：

GET http://170.187.230.78:9600/api/server/member/getUserMongoDBClusterResourceCount/{{memberId}}/{{competence}}

---

17.2 请求参数：



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| competence          |         Path           |            权限:write,read,null            |        Yes       |String        |

![img_70.png](https://github.com/whaleal/guide/blob/main/Images/img_70.png)

----

17.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |
| data       |         返回数量|                        |

![img_71.png](https://github.com/whaleal/guide/blob/main/Images/img_71.png)






---


#### 18 获取信息数据

18.1 请求路径：

GET http://170.187.230.78:9600/api/server/member/getMessageData/{{memberId}}/{{pageSize}}/{{pageIndex}}


---

18.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| pageSize          |         Path           |            每页大小            |        Yes       |Int        |
| pageIndex          |         Path           |            第几页            |        Yes       |Int        |
| operatorName          |         参数           |            操作者名称            |        No       |String        |
| objectName          |         参数           |            被操作的对象名称            |        No       |String        |
| type          |         参数           |            主机 mongodb 用户 告警            |        No       |String        |
| status          |         参数           |            状态            |        Yes       |Boolean        |
| message          |         参数           |            消息            |        No       |String        |
| startTime          |         参数           |            开始时间            |        Yes       |Long        |
| endTime          |         参数           |            结束时间            |        Yes       |Long        |

![img_72.png](https://github.com/whaleal/guide/blob/main/Images/img_72.png)

----

18.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |
| data       |         返回数据|            MessageEntity            |

![img_73.png](https://github.com/whaleal/guide/blob/main/Images/img_73.png)


---


#### 19 获取消息数量

19.1 请求路径：


GET http://170.187.230.78:9600/api/server/member/getMessageCount/{{memberId}}

---


19.2 请求参数：

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| pageSize          |         Path           |            每页大小            |        Yes       |Int        |
| pageIndex          |         Path           |            第几页            |        Yes       |Int        |
| operatorName          |         参数           |            操作者名称            |        No       |String        |
| objectName          |         参数           |            被操作的对象名称            |        No       |String        |
| type          |         参数           |            主机 mongodb 用户 告警            |        No       |String        |
| status          |         参数           |            状态            |        Yes       |Boolean        |
| message          |         参数           |            消息            |        No       |String        |
| startTime          |         参数           |            开始时间            |        Yes       |Long        |
| endTime          |         参数           |            结束时间            |        Yes       |Long        |

![img_74.png](https://github.com/whaleal/guide/blob/main/Images/img_74.png)

----

19.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |
| data     |         返回数量|                        |

![img_75.png](https://github.com/whaleal/guide/blob/main/Images/img_75.png)


---


#### 20 更新消息状态

20.1 请求路径：

GET http://170.187.230.78:9600/api/server/member/update/messageStatus/{{memberId}}/{{messageId}}

---

20.2 请求参数：


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| messageId          |         Path           |            消息id            |        Yes       |String        |

![img_76.png](https://github.com/whaleal/guide/blob/main/Images/img_76.png)

----

20.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |
| msg       |         返回消息|                        |


![img_77.png](https://github.com/whaleal/guide/blob/main/Images/img_77.png)



---


#### 21 更新所有消息状态

21.1 请求路径：

GET http://170.187.230.78:9600/api/server/member/update/allMessageStatus/{{memberId}}

---


21.2 请求参数：



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |

![img_78.png](https://github.com/whaleal/guide/blob/main/Images/img_78.png)

----

7.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |                       |
| msg       |         返回消息|                        |

![img_79.png](https://github.com/whaleal/guide/blob/main/Images/img_79.png)



---
---


##MemberMongoEntity


|       Name         |     Type             |    Description      |
| ------------       |----------            |---------------------|
| account                 |   string             |         用户名          |
| password             |   string             |         密码     |
| email              |   string |         邮箱     |
| areaCode               |   string             |         区号     |
| phone         |   string             |         手机号     |
| role           |   string             |         角色     |
| timezone             |   string             |         时区     |
| receiveAlert             |   boolean             |         是否接受警告     |
| dingDingList             |   List\<string>             |         钉钉机器人列表     |

---

##MessageEntity


|       Name         |     Type             |    Description      |
| ------------       |----------            |---------------------|
| Type                 |   string             |         消息类型          |
| objectId             |   string             |         被操作的对象id     |
| objectName              |   string |         被操作的对象名称     |
| operatorId               |   string             |         操作者id     |
| operatorName         |   string             |         操作者名称     |
| eventId           |   string             |         所属事件组     |
| List\<MessageStatus>             |   List             |         接受告警信息的人     |


---
---

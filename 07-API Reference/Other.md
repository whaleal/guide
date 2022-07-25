# Other接口
此接口调用时须在请求头中设置OPS-Token ，填写参数发起请求，返回内容为 JSON 格式的信息，返回特殊实体类将在最后提供实体类表格。



### 请求头默认格式，特殊情况特殊声明



| KEY                |     VALUE      |     
| -------------------|----------------------|
| Accept-Encoding        |         gzip, deflate, br |     
| Connection          |         keep-alive           |          
| Content-Type          |         application/json |    
---


####  1 获取所有mongo版本信息.


1.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/other/getAllMongoVersion


---

1.2 请求：


![img.png](../Images/getAllMongoVersion.png)



----

1.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |           int            |    
| data       |         返回数据         |           List              | 


<br>

![img_1.png](../Images/getAllMongoVersion_r.png)


---

<br>

###  2 获取所有whaleal版本信息.


2.1 请求路径：

GET http://{Server-Host}:{端口}/api/server/other/getWhalealVersion


---

2.2 请求：


![img_2.png](../Images/getWhalealVersion.png)



----

2.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |    
| data       |         返回消息        |           String              | 

<br>

![img_3.png](../Images/getWhalealVersion_r.png)

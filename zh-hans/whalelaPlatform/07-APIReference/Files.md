# File接口
此接口调用时须在请求头中设置whaleal-Token ，填写参数发起请求，返回内容为 JSON 格式的信息，返回特殊实体类将在最后提供实体类表格。

### 请求头默认格式，特殊情况特殊声明

    whaleal-Token在调用登录接口时返回，在之后调用接口时将token放置请求头中。
[登录接口调用获取whaleal-Token](Member.md)


| KEY                |     VALUE      |     
| -------------------|----------------------|
| Accept-Encoding        |         gzip,deflate,br |     
| Connection          |         keep-alive           |          
| Content-Type          |multipart/form-data; boundary=\<calculated when request is sent> |    
| whaleal-token          |         "token"           |     
---

<br>

###  1 上传文件到Server端


1.1 请求路径

POST: http://{Server-Host}:{端口}/api/server/file/web/upload/file

---

1.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| File          |         Body           |            上传的文件            |        Yes       |MultipartFile
| whaleal-Token          |         Params           |            token            |        Yes       |String

<br>

![img_13.png](../../images/whalealPlatformImages//uploadToServe.png)


----

1.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |    
| msg       |         返回消息         |             String           |        

<br>


![img_33.png](../../images/whalealPlatformImages//upload_r.png)



---

<br>



###  2 删除server端文件

     此处请求头的Content-Type为application/json 


2.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/file/deleteFile/{{filename}}

---

2.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| filename          |         Path           |            文件名称            |        Yes       |String        |


<br>


![img_34.png](../../images/whalealPlatformImages//deleteFile.png)


----

2.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| msg       |         返回消息         |            String            |        

<br>


![img_35.png](../../images/whalealPlatformImages//deleteFile_r.png)

---


<br>



### 3 获取server端的文件信息.

    此处请求头的Content-Type为application/json 

3.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/file/getAllMongoFile

---

3.2 请求


![img_36.png](../../images/whalealPlatformImages//getAllMongoFile.png)

----

3.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |    
| data       |         返回数据         |        JSON                |      


<br>



[comment]: <> (![img_37.png]&#40;../../images/whalealPlatformImages//getAllMongoFile_r.png&#41;)

~~~
{
    "code": 1000,
    "data": [
        {
            "createTime": 1658484806756,
            "updateTime": 1658484806756,
            "name": "mongodb-linux-x86_64-rhel70-4.2.17.tgz",
            "shortName": "mongodb-linux-x86_64-rhel70-4.2.17",
            "size": 133396543,
            "md5": "1",
            "version": null,
            "path": "/home/whaleal/server/mongodb-linux-x86_64-rhel70-4.2.17.tgz",
            "hostId": "",
            "server": true
        }
    ]
}
~~~

---

<br>

###  4 agent可以下载server端的文件



4.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/file/agent/download/{{filename}}

---

4.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| filename          |         Path           |            文件名称            |        Yes       |String        |
| agentId          |         Header           |            agentId         |        Yes       |String        |


<br>

![img_10.png](../../images/whalealPlatformImages//agentDownload.png)



----

4.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| 文件       |   返回文件 |         File              |    

<br>


[comment]: <> (![img_11.png]&#40;../../images/whalealPlatformImages//agentDownload_r.png&#41;)

---


<br>


###  5 更新server端的文件信息

    此处请求头的Content-Type为application/json 

5.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/file/agent/updateAllMongoFileToAgent

---

5.2 请求


<br>


![img_12.png](../../images/whalealPlatformImages//updateAllMongoFileToAgent.png)


----

5.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| msg       |         返回消息         |            String            |        

<br>


![img_13.png](../../images/whalealPlatformImages//updateAllMongoFileToAgent_r.png)

---


<br>



###  6 下载巡检日志



6.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/file/download/mdiag/{{clusterId}}/{{fileID}}/{{filename}}

---

6.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String        |
| fileID          |         Path           |            文件id            |        Yes       |String        |
| filename          |         Path           |            文件名称            |        Yes       |String        |
| whaleal-Token          |         Params           |            token            |        Yes       |String        |


<br>


![img_14.png](../../images/whalealPlatformImages//mdiagDownload.png)


----

6.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| mdiag       |   返回文件下载 |        File            |    

<br>


<br>



###  7 下载mongo集群文件



7.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/file/download/mongoClusterFile/{{clusterId}}/{{filename}}

---

7.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| clusterId          |         Path           |            集群id            |        Yes       |String        |
| filename          |         Path           |            文件名称            |        Yes       |String        |
| fileIdList          |         Params           |            文件id列表            |        Yes       |List        |
| whaleal-Token          |         Params           |            token            |        Yes       |String        |


<br>

![img_5.png](../../images/whalealPlatformImages//download_mongoClusterFile.png)



----

7.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| file       |   返回文件下载 |        File            |    



<br>

8.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/agent/downAgentFile/{{agentId}}/{{fileName}}

---

8.2 请求参数



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| agentId          |         Path           |            agentId            |        Yes       |String        |
| fileName          |         Path           |            文件名称            |        Yes       |String        |

<br>


![img_20.png](../../images/whalealPlatformImages//downAgentFile.png)

----

8.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| File       |         二进制流形式返回文件         |       File                 |        


---

<br>



[comment]: <> (## MongoFile)


[comment]: <> (|       Name         |     Type             |    Description      |   )

[comment]: <> (| ------------       |----------            |---------------------|)

[comment]: <> (| shortName                 |   String             |         姓          |   )

[comment]: <> (| Name             |   String             |         名     |   )

[comment]: <> (| Size              |   Long |         大小     |   )

[comment]: <> (| Md5               |   String             |         文件校验     |   )

[comment]: <> (| version         |   String             |         版本     |   )

[comment]: <> (| Path           |   String             |         路径     |   )

[comment]: <> (| hostId             |   String             |         主机id     |   )


[comment]: <> (---)

[comment]: <> (---)



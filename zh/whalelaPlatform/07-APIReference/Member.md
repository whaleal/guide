#Member接口
接口调用时须在请求头中设置whaleal-Token ，填写参数发起请求，返回内容为 JSON 格式的信息，返回特殊实体类将在最后提供实体类表格。



有些接口调用时需用到ID、memberId、messageId
~~~
Id为用户ID，在“保存新用户信息”接口处返回data里的id为用户ID。

memberId为用户ID，在“保存新用户信息”接口处返回data里的id为用户ID。

messageId为消息id，在“获取信息数据”接口处返回的实体类中的id。
~~~


### 请求头默认格式，特殊情况特殊声明
    
    whaleal-Token在调用登录接口时返回，在之后调用接口时将whaleal-Token放置请求头中。

| KEY                |     VALUE      |     
| -------------------|----------------------|
| Accept-Encoding        |         gzip,deflate,br |     
| Connection          |         keep-alive           |          
| Content-Type          |         application/json |    
| whaleal-token          |         "token"           |     



---


<br>


####  1 登录

1.1 请求路径


POST: http://{Server-Host}:{端口}/api/server/member/login

---

1.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| account          |         Body           |            账户名            |        Yes       |String        |
| password          |         Body           |            密码            |        Yes       |String        |

<br>


![img_38.png](../../images/whalealPlatformImages//login.png)

----

1.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据|       JSON                 |        
| generateAgentIdAble       |         是否有权限生成agentId         |         boolean               |        
| token       |         Token令牌         |         String               |   
| createMongoDBAble       |         是否有权限创建mongo集群         |         boolean               |   

<br>

[comment]: <> (![img_39.png]&#40;../../images/whalealPlatformImages//login_r.png&#41;)

~~~
{
    "code": 1000,
    "data": {
        "id": "62be61c7cbeff906da28f6ff",
        "createTime": 1656644040004,
        "updateTime": 1657690356662,
        "account": "chen123",
        "password": "",
        "email": "1q@q.com",
        "areaCode": "86",
        "phone": "17698999999",
        "role": "admin",
        "timezone": "Asia/Shanghai",
        "receiveAlert": true,
        "dingDingList": []
    },
    "createMongoDBAble": true,
    "generateAgentIdAble": true,
    "token": ""
}
~~~

---

<br>



#### 2 保存新用户信息.

2.1 请求路径


POST: http://{Server-Host}:{端口}/api/server/member/register

---

2.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberMongoEntity          |         Body           |            用户实体对象            |        Yes       |MemberMongoEntity        |


<br>

![img_40.png](../../images/whalealPlatformImages//register.png)



~~~
Ex. 保存新用户信息;其中 MemberMongoEntity 如下所示:
{
    "account": "chen123556",
    "password": "123456",
    "email": "123356789@qq.com",
    "phone": "17699969999"
}
~~~



----

2.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据|       JSON                 |        


<br>



[comment]: <> (![img_41.png]&#40;../../images/whalealPlatformImages//register_r.png&#41;)

~~~
{
    "code": 1000,
    "data": {
        "id": "62da7bd6239d00094230b525",
        "createTime": 1658485718459,
        "updateTime": 1658485718459,
        "account": "chen123556",
        "password": "",
        "email": "123356789@qq.com",
        "areaCode": "86",
        "phone": "17699969999",
        "role": "admin",
        "timezone": "Asia/Shanghai",
        "receiveAlert": true,
        "dingDingList": []
    }
}
~~~


---


<br>

####  3 更新用户信息


3.1 请求路径


POST: http://{Server-Host}:{端口}/api/server/member/update

---

3.2 请求参数

     



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberMongoEntity          |         Body           |            用户实体对象            |        Yes       |MemberMongoEntity        |


<br>



![img_14.png](../../images/whalealPlatformImages//updateMember.png)

~~~
Ex. 更新用户信息;其中 MemberMongoEntity 如下所示:
{
    "id": "62be61c7cbeff906da28f6ff",
    "createTime": 1659602792412,
    "updateTime": 1659605792412,
    "account": "chen123",
    "password": "",
    "email": "110236111@qq.com",
    "areaCode": "86",
    "phone": "17699999999",
    "role": "admin",
    "timezone": "A1",
    "receiveAlert": true,
    "dingDingList": [
        "_"
    ],
    "avatar": ""
}
~~~


----

3.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据|       JSON                 |        

<br>


[comment]: <> (![img_43.png]&#40;../../images/whalealPlatformImages//update_r.png&#41;)

~~~
{
    "code": 1000,
    "data": {
        "id": "62da7bd6239d00094230b525",
        "createTime": 1658485718459,
        "updateTime": 1658486089634,
        "account": "chen123556",
        "password": "",
        "email": "98765221@qq.com",
        "areaCode": "86",
        "phone": "17699954999",
        "role": "admin",
        "timezone": "Asia/Shanghai",
        "receiveAlert": true,
        "dingDingList": []
    }
}
~~~


---


<br>

#### 4 搜索用户

4.1 请求路径


POST: http://{Server-Host}:{端口}/api/server/member/findMemberData/{{pageSize}}/{{pageIndex}}

---

4.2 请求参数



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| pageSize          |         Path           |            每页大小            |        Yes       |int        |
| pageIndex          |         Path           |            第几页            |        Yes       |int        |
| map          |         Body           |            用户信息            |       Yes     |Map        |


<br>


![img_15.png](../../images/whalealPlatformImages//findMemberData.png)

~~~
Ex. 搜索用户;其中 Map 如下所示:
{
    "account": "chen",
    "phone": "176",
    "email": "11"
}
~~~


----

4.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数据|       List                 |        

<br>


[comment]: <> (![img_45.png]&#40;../../images/whalealPlatformImages//findMemberData_r.png&#41;)


~~~
{
    "code": 1000,
    "data": [
        {
            "id": "62d8b50b239d00094230b37c",
            "createTime": 1658369291763,
            "updateTime": 1658369291763,
            "account": "chen123456",
            "password": null,
            "email": "123456789@qq.com",
            "areaCode": "86",
            "phone": "17699999999",
            "role": "admin",
            "timezone": "Asia/Shanghai",
            "receiveAlert": true,
            "dingDingList": []
        }
    ]
}
~~~

---

<br>

#### 5 查询用户数量

5.1 请求路径

POST: http://{Server-Host}:{端口}/api/server/member/findMemberCount

---

5.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| map          |         Body           |            用户信息            |       Yes     |Map        |


<br>



![img_46.png](../../images/whalealPlatformImages//findMemberCount.png)

~~~
Ex. 搜索用户;其中 Map 如下所示:
{
    "account": "chen",
    "phone": "",
    "email": ""
}
~~~

----

5.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |    
| data       |         返回数量         |       long                 |        

<br>

![img_47.png](../../images/whalealPlatformImages//findMemberCount_r.png)

---


<br>

#### 6 更新接收警报

6.1 请求路径


GET: http://{Server-Host}:{端口}/api/server/member/update/receiveAlert/{{memberId}}/{{value}}

---

6.2 请求参数



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| value          |         Path           |            是否开启            |        Yes       |boolean        |


<br>

![img_48.png](../../images/whalealPlatformImages//receiveAlert.png)

----

6.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |       int                |    
| msg       |         返回消息|           String             |        

<br>

![img_49.png](../../images/whalealPlatformImages//receiveAlert_r.png)

---

<br>


#### 7 更新时区

7.1 请求路径


GET: http://{Server-Host}:{端口}/api/server/member/update/timezone/{{memberId}}

---

7.2 请求参数

    timezone:Asia/Shanghai

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| timezone          |         Params           |            时区            |        Yes       |String        |

<br>

![img_50.png](../../images/whalealPlatformImages//timezone.png)

----

7.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |       int                |    
| msg       |         返回消息|          String              |        

<br>

![img_51.png](../../images/whalealPlatformImages//timezone_r.png)



---

<br>



#### 8 更新角色


8.1 请求路径


GET: http://{Server-Host}:{端口}/api/server/member/update/role/{{memberId}}/{{value}}

---

8.2 请求参数

    value:user,admin


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| value          |         Path           |            角色            |        Yes       |String        |

<br>

![img_52.png](../../images/whalealPlatformImages//role.png)

----

8.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |            int           |    
| msg       |         返回消息|           String             |    

<br>

![img_53.png](../../images/whalealPlatformImages//role_r.png)

---

<br>



#### 9 更新是否可以创建mongodb

9.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/member/update/createMongoDBAble/{{memberId}}/{{value}}

---

9.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| value          |         Path           |            是否开启            |        Yes       |boolean        |

<br>

![img_54.png](../../images/whalealPlatformImages//update_createMongoDBAble.png)

----

9.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |    
| msg       |         返回消息|            String            |    

<br>

![img_55.png](../../images/whalealPlatformImages//update_createMongoDBAble_r.png)


---

<br>



#### 10 更新是否可以创建agentId权限

10.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/member/update/generateAgentIdAble/{{memberId}}/{{value}}

---

10.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| value          |         Path           |            是否开启            |        Yes       |boolean        |

<br>

![img_56.png](../../images/whalealPlatformImages//update_generateAgentIdAble.png)

----

10.3 返回结果


|               |     Description    |           Schema              |  
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |          int             |    
| msg       |         返回消息|         String               |    

<br>


![img_57.png](../../images/whalealPlatformImages//update_generateAgentIdAble_r.png)



---

<br>



#### 11 更新用户资源信息

11.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/member/update/userResourceInfo/{{memberId}}/{{objectId}}/{{type}}/{{value}}

---

11.2 请求参数

    value:read,write,null
    type:mongodb,host

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| objectId          |         Path           |            根据type类型提供id            |        Yes       |String        |
| type          |         Path           |            类型            |        Yes       |String        |
| value          |         Path           |            权限            |        Yes       |String        |

<br>

![img_58.png](../../images/whalealPlatformImages//update_userResourceInfo.png)

----

11.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |
| msg       |         返回消息|           String             |

<br>

![img_59.png](../../images/whalealPlatformImages//update_userResourceInfo_r.png)

---


<br>


#### 12 删除用户

12.1 请求路径


GET: http://{Server-Host}:{端口}/api/server/member/delete/user/{{memberId}}

---

12.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |


<br>


![img_60.png](../../images/whalealPlatformImages//delete_user.png)

----

12.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |
| msg       |         返回消息|             String           |

<br>

![img_61.png](../../images/whalealPlatformImages//delete_user_r.png)

---

<br>



#### 13 获取用户资源

13.1 请求路径


GET: http://{Server-Host}:{端口}/api/server/member/getUserResource/{{memberId}}

---

13.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |

<br>

![img_62.png](../../images/whalealPlatformImages//getUserResource.png)

----

13.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |
| data       |         返回数据|                   JSON     |

<br>

![img_16.png](../../images/whalealPlatformImages//getUserResource_r.png)


~~~
{
    "code": 1000,
    "data": {
        "id": "62eb99cdca0e230d4a13c423",
        "createTime": 1659607501509,
        "updateTime": 1660121964509,
        "createMongoDBAble": true,
        "generateAgentIdAble": true,
        "mongoDBClusterList": [
            {
                "id": "62eb915e32f3671236d6a0be",
                "competence": "write"
            },
            {
                "id": "62ec7ac2ca0e230d4a13c490",
                "competence": "write"
            }
        ],
        "hostList": [
            {
                "id": "62ecaf96ca0e230d4a13c75f",
                "competence": "write"
            },
            {
                "id": "62ecb027ca0e230d4a13c764",
                "competence": "write"
            }
        ]
    }
}
~~~

---


<br>


#### 14 获取用户服务数据

14.1 请求路径


GET: http://{Server-Host}:{端口}/api/server/member/getUserServerResourceData/{{memberId}}/{{competence}}/{{pageSize}}/{{pageIndex}}

---

14.2 请求参数

    competence:write,read,null

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| competence          |         Path           |            权限            |        Yes       |String        |
| pageSize          |         Path           |            每页大小            |        Yes       |int        |
| pageIndex          |         Path           |            第几页            |        Yes       |int        |
| hostName          |         Params           |            主机名称            |        No       |String        |

<br>

![img_64.png](../../images/whalealPlatformImages//getUserServerResourceData.png)

----

14.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |          int             |
| data       |         返回数据    |            List            |

<br>

![img_17.png](../../images/whalealPlatformImages//getUserServerResourceData_r.png)

~~~
{
    "code": 1000,
    "data": [
        {
            "_id": "62eb906a32f3671236d6a0af",
            "hostName": "server121",
            "osVersion": "CentOS Linux release 7.7.1908 (Core)"
        },
        {
            "_id": "62eb90ea32f3671236d6a0b7",
            "hostName": "server90",
            "osVersion": "CentOS Linux release 7.7.1908 (Core)"
        }
    ]
}

~~~


---


<br>

#### 15 获取用户服务数

15.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/member/getUserServerResourceCount/{{memberId}}/{{competence}}

---

15.2 请求参数

    competence:write,read,null

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| competence          |         Path           |            权限            |        Yes       |String        |

<br>


![img_66.png](../../images/whalealPlatformImages//getUserServerResourceCount.png)

----

15.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |
| data       |         返回数量|           long             |

<br>

![img_67.png](../../images/whalealPlatformImages//getUserServerResourceCount_r.png)

---

<br>



#### 16 获取用户mongoDB集群资源数据

16.1 请求路径


GET: http://{Server-Host}:{端口}/api/server/member/getUserMongoDBClusterResourceData/{{memberId}}/{{competence}}/{{pageSize}}/{{pageIndex}}

---

16.2 请求参数

    competence:write,read,null 

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| competence          |         Path           |            权限           |        Yes       |String        |
| pageSize          |         Path           |            每页大小            |        Yes       |int        |
| pageIndex          |         Path           |            第几页            |        Yes       |int        |
| clusterName          |         Params           |            集群名称            |        No       |String        |


<br>

![img_18.png](../../images/whalealPlatformImages//getUserMongoDBClusterResourceData.png)


----

16.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |          int             |
| data.clusterName       |         集群名称|           String             |
| data.type       |         类型:单节点,复制集,分片,纳管|       String                 |


<br>

![img_19.png](../../images/whalealPlatformImages//getUserMongoDBClusterResourceData_r.png)

---

<br>



#### 17 获取用户mongoDB集群数

17.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/member/getUserMongoDBClusterResourceCount/{{memberId}}/{{competence}}

---

17.2 请求参数

    competence:write,read,null

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| competence          |         Path           |            权限            |        Yes       |String        |
| clusterName          |         Params           |            集群名称            |        No       |String        |


<br>

![img_20.png](../../images/whalealPlatformImages//getUserMongoDBClusterResourceCount.png)

----

17.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |          int             |
| data       |         返回数量|            long            |

<br>

![img_21.png](../../images/whalealPlatformImages//getUserMongoDBClusterResourceCount_r.png)


---


<br>


#### 18 获取信息数据

18.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/member/getMessageData/{{pageSize}}/{{pageIndex}}


---

18.2 请求参数



| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| pageSize          |         Path           |            每页大小            |        Yes       |int        |
| pageIndex          |         Path           |            第几页            |        Yes       |int        |
| operatorName          |         Params           |            操作者名称            |        No       |String        |
| objectName          |         Params           |            被操作的对象名称            |        No       |String        |
| status          |         Params           |            状态            |        No       |boolean        |
| message          |         Params           |            消息            |        No       |String        |
| startTime          |         Params           |            开始时间            |        No       |long        |
| endTime          |         Params           |            结束时间            |        No       |long        |

<br>

![img_72.png](../../images/whalealPlatformImages//getMessageData.png)

----

18.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |       int                |
| data       |         返回数据|            List            |

<br>

![img_22.png](../../images/whalealPlatformImages//getMessageData_r.png)

~~~
{
    "code": 1000,
    "data": [
        {
            "id": "62fb00088e34f36c92fb013d",
            "createTime": 1660616712771,
            "updateTime": 1660616712771,
            "message": "主机:server190已宕机\r\n\t告警时间UTC:2022-08-16 02:22:56",
            "type": "alert",
            "objectId": "62f343406ccc6972abb87818",
            "objectName": "server190",
            "operatorId": null,
            "operatorName": null,
            "eventId": null,
            "list": []
        }
    ]
}

~~~

---


<br>


#### 19 获取消息数量

19.1 请求路径


GET: http://{Server-Host}:{端口}/api/server/member/getMessageCount

---


19.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| operatorName          |         Params           |            操作者名称            |        No       |String        |
| objectName          |         Params           |            被操作的对象名称            |        No       |String        |
| status          |         Params           |            状态            |        No       |boolean        |
| message          |         Params           |            消息            |        No       |String        |
| startTime          |         Params           |            开始时间            |        No       |long        |
| endTime          |         Params           |            结束时间            |        No       |long        |

<br>

![img_74.png](../../images/whalealPlatformImages//getMessageCount.png)

----

19.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |
| data     |         返回数量|             long           |

<br>

![img_75.png](../../images/whalealPlatformImages//getMessageCount_r.png)


---


<br>


#### 20 更新消息状态

20.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/member/update/messageStatus/{{memberId}}/{{messageId}}

---

20.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |
| messageId          |         Path           |            消息id            |        Yes       |String        |

<br>

![img_76.png](../../images/whalealPlatformImages//messageStatus.png)

----

20.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |         int              |
| msg       |         返回消息|           String             |


<br>

![img_77.png](../../images/whalealPlatformImages//messageStatus_r.png)



---


<br>


#### 21 更新所有消息状态

21.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/member/update/allMessageStatus/{{memberId}}

---


21.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |

<br>

![img_78.png](../../images/whalealPlatformImages//allMessageStatus.png)

----

21.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |
| msg       |         返回消息|         String               |

<br>

![img_79.png](../../images/whalealPlatformImages//allMessageStatus_r.png)

<br>

#### 22 获取所有成员id与名称

22.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/member/getAllMemberIdAndName

---


22.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberName          |         Params           |            用户名称            |        Yes       |String        |

<br>

![img_6.png](../../images/whalealPlatformImages//getAllMemberIdAndName.png)

----

22.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |
| data       |         返回数据|         List               |




<br>


~~~
{
    "code": 1000,
    "data": [
        {
            "id": "63031cb149d5ad2d50af5d15",
            "name": "admin"
        },
        {
            "id": "630321262ef5221f75e9f0c6",
            "name": "chen"
        }
    ]
}
~~~


<br>


#### 23 获取所有成员id与名称

23.1 请求路径

GET: http://{Server-Host}:{端口}/api/server/member/resetPassword/{{memberId}}

---


23.2 请求参数


| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| memberId          |         Path           |            用户id            |        Yes       |String        |

<br>

![img_7.png](../../images/whalealPlatformImages//resetPassword.png)

----

23.3 返回结果


|               |     Description    |           Schema              |
| --------------|----------------------|---------------------------
| code        |   状态符:1000成功,其余异常 |        int               |
| data       |         返回数据|         List               |




<br>

![img_8.png](../../images/whalealPlatformImages//resetPassword_r.png)

<br>























<br>

[comment]: <> (---)

[comment]: <> (---)


[comment]: <> (## MemberMongoEntity)


[comment]: <> (|       Name         |     Type             |    Description      |)

[comment]: <> (| ------------       |----------            |---------------------|)

[comment]: <> (| account                 |   String             |         用户名          |)

[comment]: <> (| password             |   String             |         密码     |)

[comment]: <> (| email              |   String |         邮箱     |)

[comment]: <> (| areaCode               |   String             |         区号     |)

[comment]: <> (| phone         |   String             |         手机号     |)

[comment]: <> (| role           |   String             |         角色     |)

[comment]: <> (| timezone             |   String             |         时区     |)

[comment]: <> (| receiveAlert             |   boolean             |         是否接受警告     |)

[comment]: <> (| dingDingList             |   List\<String>             |         钉钉机器人列表     |)

[comment]: <> (---)

[comment]: <> (## MessageEntity)


[comment]: <> (|       Name         |     Type             |    Description      |)

[comment]: <> (| ------------       |----------            |---------------------|)

[comment]: <> (| Type                 |   String             |         消息类型          |)

[comment]: <> (| objectId             |   String             |         被操作的对象id     |)

[comment]: <> (| objectName              |   String |         被操作的对象名称     |)

[comment]: <> (| operatorId               |   String             |         操作者id     |)

[comment]: <> (| operatorName         |   String             |         操作者名称     |)

[comment]: <> (| eventId           |   String             |         所属事件组     |)

[comment]: <> (| List\<MessageStatus>             |   List             |         接受告警信息的人     |)


[comment]: <> (---)

[comment]: <> (---)

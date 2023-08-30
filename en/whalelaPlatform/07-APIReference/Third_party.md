
# Third-party API
To call this API, you need to set the `whaleal-Token` in the request header with the specified parameters. The returned content is in JSON format. Special entity classes for the response will be provided in the final table.

### Default Request Header Format, Special Cases are Specified

| KEY                |     VALUE      |     
| -------------------|----------------------|
| Accept-Encoding        |         gzip, deflate, br |     
| Connection          |         keep-alive           |          
| Content-Type          |         application/json |    

### 1 Send DingTalk Message

1.1 Request Path

GET: http://{Server-Host}:{Port}/api/third/ding/sendMsg

---

1.2 Request Parameters

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| accessToken        |         Params         |       DingTalk robot token      |      Yes            |    String
| secret             |         Params         |       DingTalk robot secret     |      Yes            |    String
| content            |         Params         |       Message content           |      Yes            |    String

![img_33.png](../../../images/whalealPlatformImages/ding_sendMsg.png)

----

1.3 Response Result

|            | Description              | Schema   |
| ---------- | ------------------------ | -------- |
| code       | Status: 1000 for success, others for exceptions | int      |
| data       | Response message         | String   |

![img_32.png](../../../images/whalealPlatformImages/ding_sendMsg_r.png)

---

### 2 Send Email Message

2.1 Request Path

GET: http://{Server-Host}:{Port}/api/third/email/sendMsg

---

2.2 Request Parameters

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| email              |         Params         |       Email account             |      Yes            |    String
| content            |         Params         |       Message content           |      Yes            |    String

![img_26.png](../../../images/whalealPlatformImages/email_sendMsg.png)

----

2.3 Response Result

|            | Description              | Schema   |
| ---------- | ------------------------ | -------- |
| code       | Status: 1000 for success, others for exceptions | int      |
| data       | Response message         | String   |

![img_27.png](../../../images/whalealPlatformImages/email_sendMsg_r.png)

---

### 3 Send SMS Verification Code

3.1 Request Path

GET: http://{Server-Host}:{Port}/api/third/sms/sendMsg

---

3.2 Request Parameters

| Name                |     Located in     |           Description         |     Required    |        Schema   |
| -------------------|----------------------|-------------------------------|-----------------|-----------   |
| mobile             |         Params         |       Phone number              |      Yes            |    String
| content            |         Params         |       Message content           |      Yes            |    String

![img_28.png](../../../images/whalealPlatformImages/sms_sendMsg.png)

----

3.3 Response Result

|            | Description              | Schema   |
| ---------- | ------------------------ | -------- |
| code       | Status: 1000 for success, others for exceptions | int      |
| data       | Response message         | String   |


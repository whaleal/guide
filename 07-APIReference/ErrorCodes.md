
# ErrorCodes

    当你向接口发送请求遇到错误时，接口将返回以下错误码之一


错误码列表：
* 9: 通用 开头的code的msg不进行前端展示
* 10 ：标识正常执行的代码 无msg
* 11: 用户
* 12: agent


| Error                |     HTTP Code      |    Description| 
| -------------------|----------------------|---
| UNKNOWN_EXCEPTION      |        901        |     系统未知异常
| ERROR_SYSTEM          |         902           |     系统错误     
| LIMIT_GATEWAY         |         903            |     网关限制
| ERROR_EXE_COMMAND          |    903          |    更新命令状态失败
| SUCCESS_CODE          |        1000           |    正常执行
| NOT_EXIST_ACCOUNT          |    1101           |    账号不存在
| ERROR_PASSWORD                      |     1102              |  密码错误  
| BLANK_ACCOUNT                      |      1103             |    账号不可为空
| EXIST_PHONE                      |        1104           |    手机号已存在
| EXIST_EMAIL                      |        1105           |    邮箱已存在
| EXIST_ACCOUNT                      |      1106             |    账号已存在
| NOT_EXIST_TOKEN                      |    1107              |    TOKEN不存在
| ERROR_UPDATE_MEMBER                      |   1108                |   更新信息失败 
| NOT_EXIST_AGENT_ID                      |    1201               |    agentId不存在
| ERROR_SAVE_AGENT_LOG                      |   1202                |    日志信息保存失败
| ERROR_DOWN_LOAD_FILE                      |    1203               |    文件下载失败
| OPS_COMMON_EXCEPTION                      |   1900                |   OPS常见异常
| NOT_EXIST_DATA                      |      1901             |    数据不存在
|
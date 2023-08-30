# Error Codes

When you encounter an error while sending a request to the API, the interface will return one of the following error codes.

Error code list:
- 9: Common - Codes starting with this value are not displayed to the frontend as part of the message.
- 10: Indicates normal execution with no message (msg).
- 11: User-related errors.
- 12: Agent-related errors.

| Error                |     HTTP Code      |    Description| 
| -------------------|----------------------|---
| UNKNOWN_EXCEPTION      |        901        |     Unknown system exception
| ERROR_SYSTEM          |         902           |     System error
| LIMIT_GATEWAY         |         903            |     Gateway limitation
| ERROR_EXE_COMMAND          |    903          |    Failed to update command status
| SUCCESS_CODE          |        1000           |    Normal execution
| NOT_EXIST_ACCOUNT          |    1101           |    Account does not exist
| ERROR_PASSWORD                      |     1102              |  Incorrect password
| BLANK_ACCOUNT                      |      1103             |    Account cannot be blank
| EXIST_PHONE                      |        1104           |    Phone number already exists
| EXIST_EMAIL                      |        1105           |    Email already exists
| EXIST_ACCOUNT                      |      1106             |    Account already exists
| NOT_EXIST_TOKEN                      |    1107              |    Token does not exist
| ERROR_UPDATE_MEMBER                      |   1108                |   Failed to update information
| NOT_EXIST_AGENT_ID                      |    1201               |    AgentId does not exist
| ERROR_SAVE_AGENT_LOG                      |   1202                |    Failed to save log information
| ERROR_DOWN_LOAD_FILE                      |    1203               |    File download failed
| OPS_COMMON_EXCEPTION                      |   1900                |   Common OPS exception
| NOT_EXIST_DATA                      |      1901             |    Data does not exist
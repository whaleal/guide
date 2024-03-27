## User Management

**Create MongoDB cluster user**

Users are created in MongoDB to provide access control and security to ensure that only authorized users can access the database.



a. Click the MongoDB options button

b. Click the cluster name where you want to create the user

![1](../../../../../images/whalealPlatformImages/user1.png)

c. Click Security Management

![1](../../../../../images/whalealPlatformImages/user2.png)

d. Click User Management to create a user

![1](../../../../../images/whalealPlatformImages/user3.png)

Configure the following configuration

| Configuration items         | value                                                        |
| --------------------------- | ------------------------------------------------------------ |
| username                    | Added username                                               |
| password                    | Configure password, you can choose to generate it randomly   |
| Role                        | db; Authentication library<br>role; Select permission role   |
| Authentication mechanism    | Select the authentication mechanism, you can choose SCRAM-SHA-1 and SCRAM-SHA-256 |
| Authentication restrictions | Client source restrictions<br/>Server address restrictions   |

e. After the configuration is completed, click Confirm to create the user.


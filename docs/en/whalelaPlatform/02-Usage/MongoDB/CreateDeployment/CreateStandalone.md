## Create Standalone

```
Creating a Standalone involves the following sections:
 - Prerequisites
 - Procedure
```

Using the Whaleal Platform, you can create a Standalone instance. Standalone instances are suitable for testing and development purposes. It is not recommended to use the Standalone deployment method in a production environment due to the lack of high availability mechanisms. For production environments, it is recommended to use the [ReplicaSet](CreateReplicaSet.md) deployment method.

### Prerequisites

Before deploying a Standalone instance, ensure that the host has been managed by the Whaleal Platform. If not, please first [Add Host](../../Host/AddHost.md).

Before deploying a Standalone instance, ensure that the Whaleal Platform has an available MongoTars. If not, please first [Upload MongoTar](../UploadMongoTar.md).

### Procedure

Step 1. Navigate to the MongoDB Cluster List

a. Navigate to the left-side navigation bar.

b. Click on the "MongoDB" option.

c. Select the "MongoList" option. The page will display all the MongoDB Clusters that the user can operate on.



Step 2. Create a Standalone Instance

a. Click on the "Create Project" button on the right side.

b. Select the "Single Node" option.



Step 3. Configure the Standalone Instance

Configure the following settings on the page

| Configuration Item | Value                                                    |
| ------------------ | -------------------------------------------------------- |
| Hostname           | The host where you want to deploy the Standalone instance |
| Port               | The port to be used by the Standalone instance            |
| Data Directory     | The absolute path to the Standalone instance data files  |
| Log File           | The absolute path to the Standalone instance log output file |
| Version            | The version of the MongoTar corresponding to the Standalone instance version |
| Authentication     | true: Enable authentication, configure username and password <br> false: Disable authentication |
| Username           | If authentication is enabled, the admin user of the Standalone instance. Authentication database is `admin` and role is `root` |
| Password           | If authentication is enabled, the admin password of the Standalone instance |



Step 4. Configure Options

a. Click the "Add Option" button.

b. Select the startup configuration item to add, then click the "Confirm" button to add.

c. Set the value of the configuration item.



Step 5. Create Standalone Instance

Click the "Create" button to create the Standalone instance.
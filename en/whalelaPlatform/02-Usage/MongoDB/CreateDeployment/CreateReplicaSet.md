## Create ReplicaSet

```
Creating a ReplicaSet involves the following sections:
 - Prerequisites
 - Procedure
```

ReplicaSet deployment provides high availability mechanisms. It is recommended for production use.

Using Whaleal Platform, you can create a ReplicaSet, add ReplicaSet nodes, and scale up or down.

### Prerequisites

Before deploying a ReplicaSet, ensure that the host has been managed by the Whaleal Platform. If not, please first [Add Host](../../Host/AddHost.md).

Before deploying a ReplicaSet, ensure that the Whaleal Platform has an available MongoTars. If not, please first [Upload MongoTar](../UploadMongoTar.md).

### Procedure

Step 1. Navigate to the MongoDB Cluster List

a. Navigate to the left-side navigation bar.

b. Click on the "MongoDB" option.

c. Select the "MongoList" option. The page will display all the MongoDB Clusters that the user can operate on.



Step 2. Create a ReplicaSet

a. Click on the "Create Project" button on the right side.

b. Select the "ReplicaSet" option.



Step 3. Configure the ReplicaSet

ReplicaSet Configuration

| Configuration Item | Value                                                    |
| ------------------ | -------------------------------------------------------- |
| ReplicaSet Name    | The value of `replSetName` in the ReplicaSet configuration |
| Tags               | The value of `tag` in the ReplicaSet configuration       |
| Enable Authentication | true: Enable authentication, configure username and password <br/> false: Disable authentication |
| Username            | If authentication is enabled, the admin user of the ReplicaSet. Authentication database is `admin` and role is `root` |
| Password            | If authentication is enabled, the admin password of the ReplicaSet |

Member Configuration

| Configuration Item | Value                                                    |
| ------------------ | -------------------------------------------------------- |
| Member Type        | Member type in the ReplicaSet: <br>Member Node: The node in the ReplicaSet that holds data and has voting rights. It can be elected as the primary node.<br>Arbiter Node: A node that does not store data in the cluster and is used only for voting and elections.<br>Hidden Node: A node in the ReplicaSet that holds data and has voting rights. Configuration parameter is `hidden`.<br>Hidden Delayed Node: A node in the ReplicaSet that holds data and has voting rights. Configuration parameters are `slaveDelay` and `hidden`. |
| Hostname           | The host where you want to deploy the ReplicaSet node    |
| Port               | The port to be used by the node                           |
| Version            | The version of the MongoTar corresponding to the node version |
| Votes              | The number of votes for elections during the ReplicaSet elections |
| Priority           | The priority during the ReplicaSet elections. If priority is 0, the node cannot be elected as the primary node |
| Delay              | The time (in seconds) the node is behind the primary node, only applicable to Hidden Delayed Node |
| Build Index        | true: Build indexes in MongoDB <br>false: Do not build indexes in MongoDB |
| Data Directory     | The absolute path to the ReplicaSet data files            |
| Log File           | The absolute path to the ReplicaSet log output file      |

Cluster Configuration

| Configuration Item | Value                                                    |
| ------------------ | -------------------------------------------------------- |
| Protocol Version   | ReplicaSet replication protocol version                 |
| Chaining Allowed   | true: Allow data replication from secondary nodes <br> false: Do not allow data replication from secondary nodes |
| Write Concern Majority Journal Default | Write to majority of nodes before returning |
| Heartbeat Timeout (secs) | Time between heartbeat checks between member nodes |
| Election Timeout (ms) | Time between checks when a member is unreachable |
| CatchUp Timeout (ms) | Time for a newly elected primary node to catch up with the latest writes |
| CatchUp Takeover Delay (ms) | Time to wait before taking over when a member node leads the primary node |

Advanced Configuration

a. Click on the "Add Option" button.

b. Select the startup configuration item to add, then click the "Confirm" button to add.

c. Set the value of the configuration item.



Step 4. Create ReplicaSet

Click the "Create" button to create the ReplicaSet.
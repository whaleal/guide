## For Zabbix User

### Does WAP support creating MongoDB clusters?

WAP supports creating MongoDB clusters:

1. Create a single node：[CreateStandalone](../02-Usage/MongoDB/CreateDeployment/CreateStandalone.md)
2. Create a replica set cluster：[CreateReplicaSet](../02-Usage/MongoDB/CreateDeployment/CreateReplicaSet.md)
3. Create a sharded cluster：[CreateShardedCluster](../02-Usage/MongoDB/CreateDeployment/CreateShardedCluster.md)
4. Managed cluster：[ExistingMongoDBDeployment](../02-Usage/MongoDB/CreateDeployment/ExistingMongoDBDeployment.md)



### Does WAP support hosting existing MongoDB clusters?

WAP supports monitoring and management of existing MongoDB clusters. Add MongoDB cluster monitoring and management through [ExistingMongoDBDeployment](../02-Usage/MongoDB/CreateDeployment/ExistingMongoDBDeployment.md).

**WAP supports discovering and monitoring all nodes in the cluster through one node configuration.**



### Does WAP support operations on MongoDB clusters?

WAP provides users with all commonly used operations during use, operation and maintenance, allowing users to complete changes to the cluster through configuration and clicks on the page.



### What operations does WAP provide for MongoDB?

#### diagnostic analysis

Through combined analysis of Info, Health, Performance, LogVis, and ExplainPlan in real-time diagnostic data, we can confirm the cause of the current node problem and come up with a solution.

#### Alarm monitoring

By configuring the alarm parameter threshold, when an abnormality occurs on a node and the pressure increases, alarm information can be sent through email, SMS, DingTalk, etc. in the user configuration.

#### Data management

WAP provides a page display box to display user-defined page display of queried data, displaying data conveniently and friendlyly.

#### User Management

Display all roles and users in the cluster, and display the permissions of roles and users in detail.

#### Node management

Users can add nodes to the replica set cluster and shard cluster shard/config with one click through WAP to avoid adding failures caused by user input errors in the command line.

#### Certification management

Users can enable cluster authentication with one click through WAP, and WAP restarts the cluster in a rolling manner without affecting service usage.

#### Version changes

WAP provides rolling upgrade and downgrade operations to make version changes between **adjacent versions** of the cluster without affecting service usage.

#### Architecture changes

WAP provides the function of changing the Standalone architecture to the ReplicaSet architecture.
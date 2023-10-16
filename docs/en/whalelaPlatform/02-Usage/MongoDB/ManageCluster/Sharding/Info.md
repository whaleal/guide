## Info Sharding

```
The Info Sharding section provides the following operations:
 - Monitoring Data
 - MongoDB Logs
 - Real-time Diagnosis
 - Alert
 - Details
 - Operation
```

View Sharding node data

a. Navigate to the left-side navigation bar.

b. Click on the "MongoDB" option.

c. Select the "MongoList" option.

d. On the MongoDB static information page, click on the name of the cluster with the type "Sharded Cluster".

### Monitoring Data

View Monitoring Data

a. On the cluster information page, select node information.

b. Under node information, click on the node name (usually in the format hostname:port).

Whaleal Platform provides a rich set of monitoring metrics and allows filtering for any time range.

![image-20220722140023418](../../../../../../images/whalealPlatformImages/MongoDB_Sharding_Monitor.png)

### MongoDB Logs

View MongoDB Logs data

a. On the cluster information page, select node information.

b. Under node information, click on "View Logs".

Whaleal Platform records and stores complete MongoDB logs, providing filtering options to easily locate and diagnose issues.

![image-20220722140139512](../../../../../../images/whalealPlatformImages/MongoDB_Sharding_logs.png)

### Real-time Diagnosis

View Real-time Diagnosis data

a. On the cluster information page, select node information.

b. Under node information, click on "Real-time Diagnosis".

**Top**

Top displays hot collections at the current time.

![image-20220722140537600](../../../../../../images/whalealPlatformImages/MongoDB_Sharding_Real_time_Top.png)

**Op**

Op displays specific operation commands executed at the current time.

![image-20220722140834719](../../../../../../images/whalealPlatformImages/MongoDB_Sharding_Real_time_Op.png)

**Explain**

Explain analyzes query operation execution plans, facilitating query optimization and adjustments.

![image-20220722141114056](../../../../../../images/whalealPlatformImages/MongoDB_Sharding_Real_time_Explain.png)

### Alert

View Alert data

a. On the cluster information page, select node information.

b. Under node information, click on "Alert Monitoring".

Configure alerts for specific metrics. When triggered, alerts can be sent to users via email, SMS, DingTalk, etc.

![image-20220722141255415](../../../../../../images/whalealPlatformImages/MongoDB_Sharding_Alert.png)

### Details

View Details data

a. On the cluster information page, select node information.

b. Under node information, click on "Details".

Displays detailed node information, including creation time, version, startup command, and node configuration.

![image-20220722141402238](../../../../../../images/whalealPlatformImages/MongoDB_Sharding_Details.png)

### Operation

Perform other operations on this node, including: update node information, start node, shut down node, restart node, delete node, detach from management, enable/disable QPS monitoring, enable/disable TopAndOp monitoring, enable/disable MongoDB log collection.

* Update Node Information: By default, updates node information every 10 seconds. Click the button to trigger an immediate update and display the latest node status.

* Start Node: Click to start a stopped node.

* Shut Down Node: Click to shut down a running node.

* Restart Node: Restart a running node.

* Delete Node: Remove this node from the cluster.

* Detach from Management: Whaleal Platform will no longer monitor or manage this node.

* Enable/Disable QPS Monitoring: Choose whether to collect QPS monitoring data.

* Enable/Disable TopAndOp Monitoring: Choose whether to collect real-time diagnosis data.

* Enable/Disable MongoDB Log Collection: Choose whether to collect MongoDB log data.

![image-20220722141521552](../../../../../../images/whalealPlatformImages/MongoDB_Sharding_Operation.png)
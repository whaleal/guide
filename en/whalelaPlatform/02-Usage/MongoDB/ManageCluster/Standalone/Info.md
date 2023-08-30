## Info Standalone

```
The Info Standalone section provides the following operations:
 - Monitoring Data
 - MongoDB Logs
 - Real-time Diagnosis
 - Alert
 - Details
 - Operation
```

View Standalone node data

a. Navigate to the left-side navigation bar.

b. Click on the "MongoDB" option.

c. Select the "MongoList" option.

d. On the MongoDB static information page, click on the name of the cluster with the type "Standalone".

### Monitoring Data

View Monitoring Data

a. On the cluster information page, select the node information.

b. Under the node information, click on the node name (usually in the format hostname:port).

Whaleal Platform provides rich monitoring metrics and allows filtering within any time range.

![image-20220721132736380](../../../../../../images/whalealPlatformImages/MongoDB_Standalone_Monitor.png)

### MongoDB Logs

View MongoDB Logs Data

a. On the cluster information page, select the node information.

b. Under the node information, click on "View Logs".

Whaleal Platform records and saves complete MongoDB logs, providing filtering options to quickly locate issues.

![image-20220721171530695](../../../../../../images/whalealPlatformImages/MongoDB_Standalone_logs.png)

### Real-time Diagnosis

View Real-time Diagnosis Data

a. On the cluster information page, select the node information.

b. Under the node information, click on "Real-time Diagnosis".

**Top**

Top displays hot collections at the current time point.

![image-20220721172106803](../../../../../../images/whalealPlatformImages/MongoDB_Standalone_Real_time_Top.png)

**Op**

Op displays specific command execution at the current time.

![image-20220721172328086](../../../../../../images/whalealPlatformImages/MongoDB_Standalone_Real_time_Op.png)

**Explain**

Explain analyzes the execution plan of queries, facilitating query adjustment and optimization.

![image-20220721172503028](../../../../../../images/whalealPlatformImages/MongoDB_Standalone_Real_time_Explain.png)

### Alert

View Alert Data

a. On the cluster information page, select the node information.

b. Under the node information, click on "Alert Monitoring".

Configure alerts for specific metrics. Once triggered, users are notified via email, SMS, DingTalk, and other methods.

![image-20220721172846113](../../../../../../images/whalealPlatformImages/MongoDB_Standalone_Alert.png)

### Details

View Details Data

a. On the cluster information page, select the node information.

b. Under the node information, click on "Details".

Display detailed node information, including creation time, version, startup command, and node configuration.

![image-20220721181402943](../../../../../../images/whalealPlatformImages/MongoDB_Standalone_Details.png)

### Operation

Perform other operations on this node, including: updating node information, starting node, shutting down node, restarting node, removing node from management, enabling/disabling QPS monitoring, enabling/disabling TopAndOp monitoring, enabling/disabling MongoDB log collection.

* Update Node Information: The default interval is 10 seconds to trigger the update of node information. Click the button to trigger it immediately and display the latest node status.

* Start Node: Click to start a stopped node.

* Shutdown Node: Click to shut down a running node.

* Restart Node: Restart a running node.

* Remove from Management: Whaleal Platform will no longer monitor or manage this node.

* Enable/Disable QPS Monitoring: Choose whether to collect QPS monitoring data.

* Enable/Disable TopAndOp Monitoring: Choose whether to collect real-time diagnosis data.

* Enable/Disable MongoDB Log Collection: Choose whether to collect MongoDB log data.

![image-20220721182045976](../../../../../../images/whalealPlatformImages/MongoDB_Standalone_Operation.png)
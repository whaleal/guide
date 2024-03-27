## Find BottleNeck In MongoDB

```
Find BottleNeck In MongoDB Divided into the following two parts：
 - Find BottleNeck
 - Adjust and Optimize
```

### Find BottleNeckin

* Use MongoDB monitoring data to view indicators such as the number of node reads per second, executed commands, number of read and write waiting queues, network throughput, number of connections, etc.

* Through this performance monitoring data, you can understand the overall number of connections, the number of read and write requests, and the read and write ratio of the mongodb instance (some businesses have a high proportion of read requests, and some businesses have a high proportion of write requests).

* You need to focus on the number of read and write waiting queues. If the value exceeds 3 or exceeds the number of CPU cores, it means that CPU resources are tight and business requests have begun to backlog.

* By analyzing MongoDB real-time diagnostic data and confirming tables with higher request times, according to the 28/20 theorem, we can choose to conduct targeted performance analysis and optimization for slow queries on hot tables that take up more than 80% of the request time.

* By implementing diagnostic data, you can view the specific slow query requests executed by the current mongodb instance. For business libraries with many aggregate analysis requests, aggregate analysis statements that take more than 100 seconds are often executed from time to time. As a result, CPU and IO resources are very tight. At this time, in order not to affect the normal business process, we can only temporarily kill many accumulated slow query statements first.

### Adjust and Optimize



Mongodb sharded cluster optimization ideas:

In a sharded cluster, a certain shard has a particularly high load. (It is often the load on a certain shard that is high. If the loads on multiple shard nodes are high, you need to analyze them one by one)

* Part-1: First, use the MongoDB monitoring page to understand the approximate concurrent load and read-write ratio of the system, and observe the specific bottlenecks of the system.

* Part-2: If the load only occurs concentratedly on a certain node, use real-time diagnostic data to record tables with frequent operations.

* Part-3: Analyze the TOP10 slow queries that occur during business peak periods by implementing diagnostic data.

* Part-4: Locate the target table that needs optimization and perform query optimization.

 Usually Part-2 and Part-3 will have many identical tables. Because operations are more frequent and slow queries often exist in the same tables. These tables are the targets we need to optimize.

Mongodb sharding optimization has the following points:

 a. View information such as table sharding keys, data distribution, total data volume, and data occupied space. Focus on whether the data sharding key settings are reasonable and whether the data distribution is even;

 b. The slow query information printed in the diagnostic data contains the query conditions for each slow query. Confirm whether there is a suitable index on the slow query table that meets the query conditions. It is necessary to combine explain() to analyze the specific execution plan of the slow query.

 c. Select the original logs of the mongodb instance during the peak business period and filter the original query statements related to the slow query table. Record these original query statements to facilitate subsequent communication with development colleagues to see if corresponding optimization can be carried out based on business scenarios.

 d. For log type tables such as logs, events, session information, etc., you can retain only valid data within a certain period of time based on event fields according to business needs. Usually this needs to be clearly communicated to the development business. After confirming the retention time, you can use the mongodb TTL index feature to create an index on a specific time field and set the record expiration time limit.

* Part-5: Optimize the read-write separation in the architecture.

​	If many of the TOP10 slow queries found in Part-3 are simple queries that can effectively utilize the index, under normal circumstances, the execution should be very fast (within 200ms).

​	If it cannot be solved, you need to consider optimizing the read-write separation in the architecture. Because the high concurrent reading and writing of the hotspot table will overwhelm the CPU, causing normal queries to be blocked.

​	In short, the key to mongodb optimization is to find system bottlenecks and root causes of problems. After locating the target table that needs to be optimized, simply add an index or separate reading and writing, and performance problems are often easily solved.
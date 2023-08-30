## Find Bottleneck in MongoDB

Finding bottlenecks in MongoDB can be divided into the following two parts:

### Find Bottleneck

* Review MongoDB monitoring data to observe metrics such as reads per second, executed commands, read-write queue lengths, network throughput, and connection counts for nodes.

* Performance monitoring data provides insight into the overall connection count, read and write request counts, as well as the ratio between reads and writes for MongoDB instances.

* Pay attention to the read-write queue lengths. If this value exceeds 3 or the number of CPU cores, it indicates that CPU resources are constrained, and there is a backlog of business requests.

* Analyze MongoDB real-time diagnostic data to identify tables with high query times. Following the Pareto principle, focus on analyzing and optimizing slow queries for the "hot" tables that contribute to more than 80% of the request time.

* Examine diagnostic data to see the specific slow query requests currently executed by the MongoDB instance. For databases with frequent aggregation analysis requests, queries that take more than 100 seconds to execute might be observed. This leads to intense CPU and IO resource usage. To prevent disruptions to normal business operations, you might need to temporarily terminate many accumulated slow queries.

### Adjust and Optimize

Optimization strategies for a MongoDB sharded cluster:

If a specific shard in the sharded cluster exhibits high load:

* **Part-1**: Start by checking the MongoDB monitoring page to understand the overall concurrent load and read-write ratio of the system. Identify where the bottleneck is likely located.

* **Part-2**: If the load concentrates on a particular node, record the tables that have frequent operations using real-time diagnostic data.

* **Part-3**: Analyze the top 10 slow queries that occur during periods of high load using diagnostic data.

* **Part-4**: Identify the target tables for optimization and focus on query optimization.

Often, Part-2 and Part-3 will reveal many common tables. Frequently accessed tables and slow queries often share similar tables. These tables are your optimization targets.

Key points for MongoDB sharding optimization:

* a. Review table shard keys, data distribution, total data volume, and data storage space. Pay attention to whether the data shard key settings are appropriate and if data distribution is uniform.

* b. Examine the specific queries in the slow query information printed in the diagnostic data. Check if there are suitable indexes on the slow query tables to fulfill the query conditions. Analyze the specific execution plans of slow queries using `explain()`.

* c. Extract original query statements related to slow query tables from the original logs of the MongoDB instance during peak business periods. Record these queries for communication with development teams to discuss potential optimizations based on business scenarios.

* d. For log-type tables (logs, events, sessions, etc.), retain only valid data within a certain time frame based on business requirements. Coordinate with development teams to determine the retention period. Once determined, use MongoDB TTL index features to create an index on the specific time field and set a record expiration time.

* **Part-5**: Implement read-write separation optimization at the architecture level.

If the top 10 slow queries identified in Part-3 include queries that can effectively use indexes, the execution time should be normally fast (within 200ms). If this issue cannot be resolved, consider implementing read-write separation optimization at the architectural level. High-concurrency reads and writes to hotspot tables can overwhelm the CPU and cause blockages for normally efficient queries.

In summary, the key to MongoDB optimization is identifying system bottlenecks and root causes of problems. After pinpointing tables that require optimization, a simple addition of an index or implementation of read-write separation often effectively resolves performance issues.
### Function Operation Instructions

#### 1. Parameter Meanings
When configuring a MongoDB data synchronization task, here is the detailed meaning of each parameter:

1. **workName**:
    - Meaning: Task name
    - Description: Used to identify the name of the data synchronization task. If not provided, it defaults to "workNameDefault".

2. **sourceDsUrl**:
    - Meaning: Source MongoDB connection URL
    - Description: Specifies the connection URL of the source MongoDB database, which can be a single node, a replica set, or a sharded cluster.

3. **targetDsUrl**:
    - Meaning: Target MongoDB connection URL
    - Description: Specifies the connection URL of the target MongoDB database, which can be a single node, a replica set, or a sharded cluster.

4. **syncMode**:
    - Meaning: Synchronization mode
    - Description: Specifies the mode of data synchronization, which can be one of the following options:
        - "all": Full mode, sync all tables, excluding operations on source tables during synchronization.
        - "allAndRealTime": Full plus real-time mode, performs full sync first and then starts real-time sync.
        - "allAndIncrement": Full plus incremental mode, performs full sync first and then syncs only operations on source tables during synchronization.
        - "realTime": Real-time mode, syncs based on configured start and end times.

5. **realTimeType**:
    - Meaning: Real-time task type
    - Description: Selects the type of real-time task, which can be "oplog" or "changestream".
    - Additional Information:
        - "oplog": Uses MongoDB's oplog for real-time synchronization, suitable for source replica sets, supports DDL operations, and is faster.
        - "changestream": Uses MongoDB's changestream for real-time synchronization, suitable for source replica sets or mongos, does not support DDL operations, and has moderate speed.

6. **fullType**:
    - Meaning: Full task type
    - Description: Selects the type of full task, which can be "sync" or "reactive".
    - Additional Information:
        - "sync": Uses a stable transmission method for full synchronization.
        - "reactive": Uses a faster transmission method for full synchronization.

7. **dbTableWhite**:
    - Meaning: Tables to synchronize
    - Description: Specifies tables to synchronize using regular expressions. For example, to sync all tables under the mongodb database: mongodb\\..+, the default is to sync all tables.

8. **ddlFilterSet**:
    - Meaning: DDL operations to synchronize
    - Description: Specifies DDL operations to synchronize, separated by commas. The default is *, meaning sync all DDL operations.

9. **sourceThreadNum**:
    - Meaning: Source task thread number (full mode)
    - Description: Specifies the number of threads to read source tasks in full synchronization.

10. **targetThreadNum**:
    - Meaning: Target task thread number (full mode)
    - Description: Specifies the number of threads to write target tasks in full synchronization.

... (Continues with the rest of the parameter explanations)

#### 2. Parameter Usage Scope
```
| Parameter           | Real-Time Task | Full Task | Full + Increment Task | Full + Real-Time Task |
|--------------------|--------------|----------|----------------------|-----------------------|
| workName           | ✔️           | ✔️       | ✔️                   | ✔️                    |
| sourceDsUrl        | ✔️           | ✔️       | ✔️                   | ✔️                    |
| targetDsUrl        | ✔️           | ✔️       | ✔️                   | ✔️                    |
| syncMode           | ✔️           | ✔️       | ✔️                   | ✔️                    |
| realTimeType       | ✔️           |          | ✔️                   | ✔️                    |
| fullType           |              | ✔️       | ✔️                   | ✔️                    |
| dbTableWhite       | ✔️           | ✔️       | ✔️                   | ✔️                    |
| ddlFilterSet       | ✔️           |          | ✔️                   | ✔️                    |
| batchSize          | ✔️           | ✔️       | ✔️                   | ✔️                    |
| bucketNum          | ✔️           | ✔️       | ✔️                   | ✔️                    |
| bucketSize         | ✔️           | ✔️       | ✔️                   | ✔️                    |
| startOplogTime     | ✔️           |          |                      |                       |
| endOplogTime       | ✔️           |          | ✔️                   | ✔️                    |
| delayTime          | ✔️           |          |                      |                       |
| nsBucketThreadNum  | ✔️           |          |                      |                       |
| writeThreadNum     | ✔️           |          |                      |                       |
| ddlWait            | ✔️           | ✔️       | ✔️                   | ✔️                    |
| clusterInfoSet     | ✔️           | ✔️       | ✔️                   | ✔️                    |
| bind_ip            | ✔️           | ✔️       | ✔️                   | ✔️                    |
```

#### 3. Data Validation
```
# Data validation script
# 0: Multi-threaded validation: Configure 1-8 validation methods after 0, which can be processed concurrently
# 1: Estimate count validation for libraries and tables (may be inaccurate)
# 2: Accurate count validation for libraries and tables
# 3: Library and table dbHash validation (locks the library, use with caution)
# 4: Validate 100 randomly selected data from libraries and tables, source side randomly selects 100 data, check if they exist on the target side
# 5: Validate 100 data of each data type from libraries and tables, extract 100 data of each data type for _id (first 50 and last 50), check if they exist on the target side
# 6: Check missing index information in libraries and tables
# 7: Check missing index information in libraries and tables and create missing indexes
# 8: Library dbHash validation (locks the library, use with caution)
# 9: Output detailed validation log information. When not specified, the log only records abnormal validation information
# Can be used in combination, e.g., 123456 123457 1237. If not specified, the default is combination 16
checkData=12456
```


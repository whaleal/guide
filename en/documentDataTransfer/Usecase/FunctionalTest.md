# Full Data Transfer

#### 1. Start Preparation

```
use photon
Create ten tables. Each table has no indexes other than _id.
Insert approximately 50 million records into each table.
```

#### 2. Source-side Data Insertion

```
Single record:
{
    "_id": ObjectId("61bad4f68a27d20b123ed7e8"),
    "BsonTimestamp1": Timestamp(1639634166, 78),
    "String": "str",
    "Doc": {
        "1": 1
    },
    "javaInt": 71916,
    "bytes": BinData(0, "AQ=="),
    "Array": [],
    "Binary data": BinData(0, "AQID"),
    "ObjectId": ObjectId("61bad4f68a27d20b123ed7e6"),
    "Boolean": false,
    "Date": ISODate("2021-12-16T05:56:06.688Z"),
    "Null": null,
    "Regular Expression": /lhp.*/,
    "DBPointer": DBPointer("1", ObjectId("61bad4f68a27d20b123ed7e7")),
    "Undefined": undefined,
    "JavaScript": {
        "code": "var i=0"
    },
    "Symbol": "var i=0",
    "BsonStr": "var i=0",
    "BsonJavaScriptWithScope": {
        "code": "var i=0",
        "scope": {}
    },
    "32integer": 12,
    "Timestamp": ISODate("2021-12-16T05:56:06.688Z"),
    "64int": NumberLong(123),
    "Min key": { "$minKey": 1 },
    "Max key": { "$maxKey": 1 },
    "BsonTimestamp": Timestamp(1639634166, 457)
}
```

#### 3. Source-side Data Volume Calculation

```
show dbs;
Disk usage on source: photon 35.885GB
db.stats()
{
    "db": "photon",
    "collections": 10,
    "views": 0,
    "objects": 474281344, // Estimated total number of records
    "avgObjSize": 132.06465577958498, // Average size per record in bytes
    "dataSize": 57890360946,
    "storageSize": 14807171072,
    "freeStorageSize": 4571136,
    "indexes": 20,
    "indexSize": 23723704320,
    "indexFreeStorageSize": 14454784,
    "totalSize": 38530875392,
    "totalFreeStorageSize": 19025920,
    "scaleFactor": 1,
    "fsUsedSize": 587772825600,
    "fsTotalSize": 11939478503424,
    "ok": 1,
    "$clusterTime": {
        "clusterTime": Timestamp(1640065750, 1),
        "signature": {
            "hash": BinData(0, "v3ySiE7Zub+VPOJpQ/K3IaCJBxM="),
            "keyId": NumberLong("7025843880893349893")
        }
    },
    "operationTime": Timestamp(1640065750, 1)
}
```

#### 4. Start DDT

Refer to [QuickStart](../Install/QuickStart.md)

Test environment using the following parameters:

```

# DDT.properties Configuration File
# Task name. If not specified, defaults to workNameDefault.
workName = mongoTask
# Source-side MongoDB URL, required. Can be a URL for a single node, replica set, or sharded cluster.
sourceDsUrl = mongodb://192.168.12.200:24578
# sourceDsUrl = mongodb://192.168.12.100:3999
# Target-side MongoDB URL, required. Can be a URL for a single node, replica set, or sharded cluster.
targetDsUrl = mongodb://192.168.12.100:24578
# Synchronization mode, default is all.
# all: Full data transfer, synchronizes tables while ignoring operations on the source during synchronization.
syncMode = all
# During full data transfer, choose between sync or reactive.
# sync: Stable data transfer.
# reactive: Faster data transfer.
fullType = reactive
# Tables to be synchronized, using regular expressions. Default is to synchronize all tables: .+
dbTableWhite = .+
# Number of threads for reading source data during full data transfer, minimum is 2, maximum is 100. Default is system-calculated value.
sourceThreadNum = 10
# Number of threads for writing data to the target during full data transfer, minimum is 4, maximum is 100. Default is system-calculated value. It's recommended that targetThreadNum is three times sourceThreadNum.
targetThreadNum = 20
# Number of threads for concurrent index creation during full data transfer, minimum is 1, maximum is 100. Default is system-calculated value.
createIndexThreadNum = 15
# The following three parameters, bucketSize, bucketNum, and batchSize, collectively determine the number of data records cached in memory during full data transfer. Be cautious about potential memory overflow.
# Default batchSize is 128.
batchSize = 128
# Default bucketNum is 20.
bucketNum = 20
# Default bucketSize is 20.
bucketSize = 20
# Maximum time allowed for each DDL operation during synchronization, in seconds.
ddlWait = 1200
# During full data transfer:
# Before data transmission, pre-process: synchronize DDL information in the cluster.
# 0: Whether to delete existing tables on the target.
# 1: Print all user information in the cluster.
# 2: Synchronize table structure.
# 3: Synchronize table index information.
# 4: Enable sharding for all databases.
# 5: Synchronize shard key for tables.
# 6: Synchronize config.setting table.
# 7: Pre-split chunk for tables.
# Combine numbers using commas. For example: 1,2,3,4,5,6.
clusterInfoSet = 0,1,2,3,4,5,6,7
# When monitor is enabled, configure the IP address of the local machine.
bind_ip = 192.168.12.190

```


# Real-time

#### 1. Start DDT

Refer to [QuickStart](../Install/QuickStart.md)

Test environment using the following parameters:

```
# DDT.properties Configuration File
# Task name. If not specified, defaults to workNameDefault.
workName = mongoTask
# Source-side MongoDB URL, required. Can be a URL for a single node, replica set, or sharded cluster.
sourceDsUrl = mongodb://192.168.12.200:24578
# sourceDsUrl = mongodb://192.168.12.100:3999
# Target-side MongoDB URL, required. Can be a URL for a single node, replica set, or sharded cluster.
targetDsUrl = mongodb://

192.168.12.100:24578
# Synchronization mode, default is all.
# realTime: Real-time synchronization. startOplogTime and endOplogTime can be configured.
syncMode = realTime
# Choose between oplog and changestream for real-time or incremental tasks.
# Choose oplog for advantages such as faster synchronization speed when the source is a replica set and support for DDL operations.
# Choose changestream for sources that are replica sets or mongos, but it doesn't support DDL operations and is generally slower.
realTimeType = changestream
# Tables to be synchronized, using regular expressions. Default is to synchronize all tables: .+
dbTableWhite = .+
# In real-time synchronization, you can specify which DDL operations to synchronize: drop, create, createIndexes, dropIndexes, renameCollection, convertToCapped, dropDatabase, modify, shardCollection.
# Default is *, which means all DDL operations are synchronized.
ddlFilterSet = *
# The following three parameters, bucketSize, bucketNum, and batchSize, collectively determine the number of data records cached in memory during real-time synchronization. Be cautious about potential memory overflow.
# Default batchSize is 128.
batchSize = 128
# Default bucketNum is 20.
bucketNum = 20
# Default bucketSize is 20.
bucketSize = 20
# When using real-time synchronization, set the start time to read oplog. Default is the 10-digit timestamp when the program starts.
startOplogTime = 1692843646
# When using real-time synchronization, set the end time to read oplog. Default is 0, meaning no end time. Use a 10-digit timestamp if needed.
endOplogTime = 1692847246
# When using real-time synchronization, set the delay time for reading oplog. Default is 0, meaning no delay time.
delayTime = 0
# Number of threads for parsing namespaces (buckets) during real-time synchronization. Minimum is 8, maximum is 100. Default is system-calculated value.
nsBucketThreadNum = 15
# Number of threads for writing data during real-time synchronization. Minimum is 8, maximum is 100. Default is system-calculated value.
writeThreadNum = 15
# Maximum time allowed for each DDL operation during synchronization, in seconds.
ddlWait = 1200
# When monitor is enabled, configure the IP address of the local machine.
bind_ip = 192.168.12.190

```

#### 2. Source-side Data Insertion

```
Use the source-side script for CRUD operations.
The script performs CRUD operations on 10 tables.
Single insert data model:
{
    "_id": ObjectId("61bad4f68a27d20b123ed7e8"),
    "BsonTimestamp1": Timestamp(1639634166, 78),
    "String": "str",
    "Doc": {
        "1": 1
    },
    "javaInt": 71916,
    "bytes": BinData(0, "AQ=="),
    "Array": [],
    "Binary data": BinData(0, "AQID"),
    "ObjectId": ObjectId("61bad4f68a27d20b123ed7e6"),
    "Boolean": false,
    "Date": ISODate("2021-12-16T05:56:06.688Z"),
    "Null": null,
    "Regular Expression": /lhp.*/,
    "DBPointer": DBPointer("1", ObjectId("61bad4f68a27d20b123ed7e7")),
    "Undefined": undefined,
    "JavaScript": {
        "code": "var i=0"
    },
    "Symbol": "var i=0",
    "BsonStr": "var i=0",
    "BsonJavaScriptWithScope": {
        "code": "var i=0",
        "scope": {}
    },
    "32integer": 12,
    "Timestamp": ISODate("2021-12-16T05:56:06.688Z"),
    "64int": NumberLong(123),
    "Min key": { "$minKey": 1 },
    "Max key": { "$maxKey": 1 },
    "BsonTimestamp": Timestamp(1639634166, 457)
}
Source-side CRUD concurrency is 100,000/s.

```

#### 3. Conclusion

During real-time synchronization, the source-side CRUD concurrency is 100,000/s.

The target-side executes an average of 58,000 data records per second.

When the data volume of source-side CRUD operations is large, it may cause DDT to be unable to synchronize the source oplog in a timely manner. Observe the 'Reading oplog delay xxxs' data and avoid missing the sliding window time for reading oplog.
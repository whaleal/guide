# DDT Real-time Testing

## Test Environment

**Hardware Configuration:**

* CPU: 40 cores, Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz
* Memory: 4*32GB
* Network Card: 1Gbps
* Operating System: Linux x86_64
* MongoDB Version: 0.1
* Disk: SSD

**Test Conditions**

The test data covers the following dimensions: Latency, QPS (Queries Per Second), CPU Usage, Memory Usage. All values are given as the average over a 10-second period.

QPS is obtained from the data platform's log output, which counts the number of OPLOG writes per second. We also provide CPU and memory usage information.

## Test Results

    When cacheBucketSize=16, cacheBucketNum=16, dataBatchSize=128:

### Test 1

**Configuration**

| Parameter                 | Description                             |
|--------------------------|-----------------------------------------|
| MongoDB Type             | Source MongoDB: Single-node replica set, cacheSize30GB  Target MongoDB: Single-node replica set, cacheSize30GB |
| Data Volume              | One database with 10 collections, each document contains 7 columns, and the total size of each document is approximately 140 bytes |
| Real-time Sync Threads   | {oplogNS=1, oplogWrite=6, oplogRead=1, oplogNsBucket=2} |
| Cache Area               | cacheBucketSize=16, cacheBucketNum=16, dataBatchSize=128 |

**Test Results**

| Measurement  | Description |
|--------------|-------------|
| QPS          | 72398       |
| CPU Usage    | 280%        |
| Memory Usage | 8258MB      |

------------

### Test 2

**Configuration**

| Parameter                 | Description                             |
|--------------------------|-----------------------------------------|
| MongoDB Type             | Source MongoDB: Single-node replica set, cacheSize30GB  Target MongoDB: Single-node replica set, cacheSize30GB |
| Data Volume              | One database with 10 collections, each document contains 7 columns, and the total size of each document is approximately 140 bytes |
| Real-time Sync Threads   | {oplogNS=1, oplogWrite=9, oplogRead=1, oplogNsBucket=3} |
| Cache Area               | cacheBucketSize=16, cacheBucketNum=16, dataBatchSize=128 |

**Test Results**

| Measurement  | Description |
|--------------|-------------|
| QPS          | 80385       |
| CPU Usage    | 240%        |
| Memory Usage | 14418MB     |

-------------

### Test 3

**Configuration**

| Parameter                 | Description                             |
|--------------------------|-----------------------------------------|
| MongoDB Type             | Source MongoDB: Single-node replica set, cacheSize30GB  Target MongoDB: Single-node replica set, cacheSize30GB |
| Data Volume              | One database with 10 collections, each document contains 7 columns, and the total size of each document is approximately 140 bytes |
| Real-time Sync Threads   | {oplogNS=1, oplogWrite=12, oplogRead=1, oplogNsBucket=4} |
| Cache Area               | cacheBucketSize=16, cacheBucketNum=16, dataBatchSize=128 |

**Test Results**

| Measurement  | Description |
|--------------|-------------|
| QPS          | 79365       |
| CPU Usage    | 280%        |
| Memory Usage | 15728MB     |

------------

### Test 4

**Configuration**

| Parameter                 | Description                             |
|--------------------------|-----------------------------------------|
| MongoDB Type             | Source MongoDB: Single-node replica set, cacheSize30GB  Target MongoDB: Single-node replica set, cacheSize30GB |
| Data Volume              | One database with 10 collections, each document contains 7 columns, and the total size of each document is approximately 140 bytes |
| Real-time Sync Threads   | {oplogNS=1, oplogWrite=15, oplogRead=1, oplogNsBucket=5} |
| Cache Area               | cacheBucketSize=16, cacheBucketNum=16, dataBatchSize=128 |

**Test Results**

| Measurement  | Description |
|--------------|-------------|
| QPS          | 75388       |
| CPU Usage    | 280%        |
| Memory Usage | 14025MB     |

### Summary

<table>
  <tr>
    <th>Cache Area</th>
    <th>oplogNS</th>
    <th>oplogWrite</th>
    <th>oplogRead</th>
    <th>oplogNsBucket</th>
    <th>QPS</th>
    <th>CPU Usage</th>
    <th>Memory Usage</th>
  </tr>
  <tr>
    <td rowspan="4">cacheBucketSize=16 cacheBucketNum=16 dataBatchSize=128</td>
    <td>1</td>
    <td>6</td>
    <td>1</td>
    <td>2</td>
    <td>72398</td>
    <td>280%</td>
    <td>8258MB</td>
  </tr>
  <tr>
    <td>1</td>
    <td>9</td>
    <td>1</td>
    <td>3</td>
    <td>80385</td>
    <td>240%</td>
    <td>14418MB</td>
  </tr>
  <tr>
    <td>1</td>
    <td>12</td>
    <td>1</td>
    <td>4</td>
    <td>79365</td>
    <td>280%</td>
    <td>15728MB</td>
  </tr>
  <tr>
    <td>1</td>
    <td>15</td>
    <td>1</td>
    <td>5</td>
    <td>75388</td>
    <td>280%</td>
    <td>14025MB</td>
  </tr>
</table>

![img_17.png](../../../images/documentDataTransferImages/img_17.png)
![img_18.png](../../../images/documentDataTransferImages/img_18.png)

Summary: When cacheBucketSize=16, cacheBucketNum=16, dataBatchSize=128, it can be observed that increasing the number of threads does not increase QPS, due to the limitation of the cache area size.

---------

    When cacheBucketSize=32, cacheBucketNum=32, dataBatchSize=128:

### Test 1

**Configuration**

| Parameter                 | Description                             |
|--------------------------|-----------------------------------------|
| MongoDB Type             | Source MongoDB: Single-node replica set, cacheSize30GB  Target MongoDB: Single-node replica set, cacheSize30GB |
| Data Volume              | One database with

10 collections, each document contains 7 columns, and the total size of each document is approximately 140 bytes |
| Real-time Sync Threads   | {oplogNS=1, oplogWrite=6, oplogRead=1, oplogNsBucket=2} |
| Cache Area               | cacheBucketSize=32, cacheBucketNum=32, dataBatchSize=128 |

**Test Results**

| Measurement  | Description |
|--------------|-------------|
| QPS          | 87719       |
| CPU Usage    | 240%        |
| Memory Usage | 13107MB     |

----------

### Test 2

**Configuration**

| Parameter                 | Description                             |
|--------------------------|-----------------------------------------|
| MongoDB Type             | Source MongoDB: Single-node replica set, cacheSize30GB  Target MongoDB: Single-node replica set, cacheSize30GB |
| Data Volume              | One database with 10 collections, each document contains 7 columns, and the total size of each document is approximately 140 bytes |
| Real-time Sync Threads   | {oplogNS=1, oplogWrite=9, oplogRead=1, oplogNsBucket=3} |
| Cache Area               | cacheBucketSize=32, cacheBucketNum=32, dataBatchSize=128 |

**Test Results**

| Measurement  | Description |
|--------------|-------------|
| QPS          | 100000      |
| CPU Usage    | 320%        |
| Memory Usage | 11534MB     |

---------

### Test 3

**Configuration**

| Parameter                 | Description                             |
|--------------------------|-----------------------------------------|
| MongoDB Type             | Source MongoDB: Single-node replica set, cacheSize30GB  Target MongoDB: Single-node replica set, cacheSize30GB |
| Data Volume              | One database with 10 collections, each document contains 7 columns, and the total size of each document is approximately 140 bytes |
| Real-time Sync Threads   | {oplogNS=1, oplogWrite=12, oplogRead=1, oplogNsBucket=4} |
| Cache Area               | cacheBucketSize=32, cacheBucketNum=32, dataBatchSize=128 |

**Test Results**

| Measurement  | Description |
|--------------|-------------|
| QPS          | 112370      |
| CPU Usage    | 320%        |
| Memory Usage | 11796MB     |

----------

### Test 4

**Configuration**

| Parameter                 | Description                             |
|--------------------------|-----------------------------------------|
| MongoDB Type             | Source MongoDB: Single-node replica set, cacheSize30GB  Target MongoDB: Single-node replica set, cacheSize30GB |
| Data Volume              | One database with 10 collections, each document contains 7 columns, and the total size of each document is approximately 140 bytes |
| Real-time Sync Threads   | {oplogNS=1, oplogWrite=15, oplogRead=1, oplogNsBucket=5} |
| Cache Area               | cacheBucketSize=32, cacheBucketNum=32, dataBatchSize=128 |

**Test Results**

| Measurement  | Description |
|--------------|-------------|
| QPS          | 120030      |
| CPU Usage    | 360%        |
| Memory Usage | 12845MB     |

### Summary

<table>
  <tr>
    <th>Cache Area</th>
    <th>oplogNS</th>
    <th>oplogWrite</th>
    <th>oplogRead</th>
    <th>oplogNsBucket</th>
    <th>QPS</th>
    <th>CPU Usage</th>
    <th>Memory Usage</th>
  </tr>
  <tr>
    <td rowspan="4">cacheBucketSize=32 cacheBucketNum=32 dataBatchSize=128</td>
    <td>1</td>
    <td>6</td>
    <td>1</td>
    <td>2</td>
    <td>87719</td>
    <td>240%</td>
    <td>13107MB</td>
  </tr>
  <tr>
    <td>1</td>
    <td>9</td>
    <td>1</td>
    <td>3</td>
    <td>100000</td>
    <td>320%</td>
    <td>11534MB</td>
  </tr>
  <tr>
    <td>1</td>
    <td>12</td>
    <td>1</td>
    <td>4</td>
    <td>112370</td>
    <td>320%</td>
    <td>11796MB</td>
  </tr>
  <tr>
    <td>1</td>
    <td>15</td>
    <td>1</td>
    <td>5</td>
    <td>120030</td>
    <td>360%</td>
    <td>12845MB</td>
  </tr>
</table>

![img_19.png](../../../images/documentDataTransferImages/img_19.png)
![img_20.png](../../../images/documentDataTransferImages/img_20.png)

Summary: When cacheBucketSize=32, cacheBucketNum=32, dataBatchSize=128, it can be observed that increasing the number of threads increases QPS, due to the limitation of the Oplog read rate.

## Conclusion:

(1) CPU vs. QPS:

![img_23.png](../../../images/documentDataTransferImages/img_23.png)

(2) Memory Usage vs. QPS:

![img_24.png](../../../images/documentDataTransferImages/img_24.png)

Make the necessary translation adjustments and ensure that the formatting and image paths are not modified.
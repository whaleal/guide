# 全量

#### 1.开始准备

```
use photon
创建十张表。每个表均无_id以为的索引
每张表插入5千万条数据左右
```

#### 2.源端插入数据

```
单条记录
{
	"_id" : ObjectId("61bad4f68a27d20b123ed7e8"),
	"BsonTimestamp1" : Timestamp(1639634166, 78),
	"String" : "str",
	"Doc" : {
		"1" : 1
	},
	"javaInt" : 71916,
	"bytes" : BinData(0,"AQ=="),
	"Array" : [ ],
	"Binary data" : BinData(0,"AQID"),
	"ObjectId" : ObjectId("61bad4f68a27d20b123ed7e6"),
	"Boolean" : false,
	"Date" : ISODate("2021-12-16T05:56:06.688Z"),
	"Null" : null,
	"Regular Expression" : /lhp.*/,
	"DBPointer" : DBPointer("1", ObjectId("61bad4f68a27d20b123ed7e7")),
	"Undefined" : undefined,
	"JavaScript" : {
		"code" : "var i=0"
	},
	"Symbol" : "var i=0",
	"BsonStr" : "var i=0",
	"BsonJavaScriptWithScope" : {
		"code" : "var i=0",
		"scope" : {

		}
	},
	"32integer" : 12,
	"Timestamp" : ISODate("2021-12-16T05:56:06.688Z"),
	"64int" : NumberLong(123),
	"Min key" : { "$minKey" : 1 },
	"Max key" : { "$maxKey" : 1 },
	"BsonTimestamp" : Timestamp(1639634166, 457)
}
```

#### 3.源端数据量计算

```
show dbs;
源端占用磁盘量 photon  35.885GB
db.stats()
{
	"db" : "photon",
	"collections" : 10,
	"views" : 0,
	"objects" : 474281344, // 总条数（大致）
	"avgObjSize" : 132.06465577958498,// 每条数据大小 单位bytes
	"dataSize" : 57890360946,
	"storageSize" : 14807171072,
	"freeStorageSize" : 4571136,
	"indexes" : 20,
	"indexSize" : 23723704320,
	"indexFreeStorageSize" : 14454784,
	"totalSize" : 38530875392,
	"totalFreeStorageSize" : 19025920,
	"scaleFactor" : 1,
	"fsUsedSize" : 587772825600,
	"fsTotalSize" : 11939478503424,
	"ok" : 1,
	"$clusterTime" : {
		"clusterTime" : Timestamp(1640065750, 1),
		"signature" : {
			"hash" : BinData(0,"v3ySiE7Zub+VPOJpQ/K3IaCJBxM="),
			"keyId" : NumberLong("7025843880893349893")
		}
	},
	"operationTime" : Timestamp(1640065750, 1)
}
```

#### 4.启动D2T

参考[QuickStart](../Install/快速启动.md)

该测试环境使用如下参数

```

# D2T.properties 配置文件
#任务名。不写则默认生成
taskName=mongoTask
#程序名名。不写则默认生成
proName=mongoPro
#source端mongodb的url。必写
sourceDsUrl=mongodb://root:123456@192.168.3.190:27001/admin
#target端mongodb的url。必写
targetDsUrl=mongodb://root:123456@192.168.3.100:47018/admin
#同步模式,默认为all
# 全量:all  全量同步表,不同步同步期间对源表进行的操作
# 全量和实时:allAndRealTime  全量同步后,开始进行实时同步,实时同步的开始时间为全量同步的开始时间
# 全量和增量:allAndIncrement 全量同步后,仅同步同步期间对源表进行的操作。增量同步的开始时间为全量同步的开始时间,增量同步的结束时间为全量同步的结束时间
# 实时:realTime 实时同步
# 注全量和增量同步是一种特殊的全量和实时同步模式
syncMode=allAndRealTime
#全量同步时,是否按照依次同步表或多表并行同步。默认为false即多表并行同步
parallelSynchronizationMultipleTables=false
#需要同步的表,使用正则表达式书写。例如同步mongodb库下的所有表：mongodb\\..+   默认同步全部表：.+
dbTableWhite=photon\\..+
# 需要同步的DDL
# 实时同步情况下可以同步drop,create,createIndexes,dropIndexes,renameCollection,convertToCapped,dropDatabase。默认值为*,即同步所有DDL操作
# 多个DDL中间使用英文逗号隔离。若多个DDL中包含*,则同步所有DDL操作
ddlFilterSet=*
#全量同步情况下:是否删除目标库已经存在的源表。默认false即不删除
autoDropExistDbTable=true
#全量同步情况下:是否同步源表的索引信息。默认true即同步。在true时,当源表数据同步60%时开始同步源表的索引
autoCreateIndex=true
#全量同步情况下读取源表的线程数。最小为2，最大为50。默认值为2
sourceThreadNum=4
#全量同步情况下执行写入目标库的线程数。最小为4，最大为50 。默认值为6
#建议targetThreadNum是sourceThreadNum的3倍
targetThreadNum=12
##下面三个参数cacheBucketSize,cacheBucketNum,dataBatchSize共同决定全量情况下,内存中缓存的数据条数,注意内存溢出的情况。
##均采用默认值则内存缓存20*20*128条数据,若每条数据100kb,则最大占用内存4.88G
#每个缓存桶缓存批次数量。默认为20
cacheBucketSize=10
#缓存区个数。默认为20
cacheBucketNum=60
#每批次数据的大小。默认为128
dataBatchSize=128
#在实时同步时,设置读取oplog的开始时间。默认值为程序启动时刻的10位时间戳，否则则书写10位时间戳
startOplogTime=
#在实时同步时,设置读取oplog的结束时间。默认值为0即没有结束时间，否则则书写10位时间戳
endOplogTime=
#在实时同步时,设置读取oplog的延迟时间。默认值为0即没有延迟时间
delayTime=
#在实时同步中每个数据源解析数据的线程。最小为4，最大为50。默认值为8
realTimeThreadNum=15
#allAndRealTime模式下,全量和实时轮转进行。每次轮转时间rotationTime单位秒s，默认为0即不进行轮转
#先全量，再实时 性能佳但是可能出现oplog被覆盖。轮转 性能不佳,oplog一般情况下不被覆盖
#rotationTime=0
```

#### 5.查看D2T运行情况

```
cd D2T
tail -f logs/log.log

 INFO  -- Program:mongoPro,当前读取Source线程数:9
 INFO  -- Program:mongoPro,总读取Source任务数:256
 INFO  -- Program:mongoPro,剩余读取Source任务数:199
 INFO  -- Program:mongoPro,sys系统线程数:0
 INFO  -- Program:mongoPro,target写入线程数:12
 INFO  -- Program:mongoPro,当前缓存区剩余批数量:600
 INFO  -- Program:mongoPro,总传输数量:474281344,已写入条数:84511016,用时:1171s,平均写入速度:72169 per/s
 INFO  -- Program:mongoPro,本轮(10s)平均写入速度:91052 per/s
 INFO  -- Program:mongoPro,状态:2
 INFO  -- Program:mongoPro,预估同步情况:18.75%,用时1171s
 
 
 
 INFO  -- Program:mongoPro,当前读取Source线程数:0
 INFO  -- Program:mongoPro,总读取Source任务数:256
 INFO  -- Program:mongoPro,剩余读取Source任务数:0
 INFO  -- Program:mongoPro,sys系统线程数:0
 INFO  -- Program:mongoPro,target写入线程数:12
 INFO  -- Program:mongoPro,当前缓存区剩余批数量:0
 INFO  -- Program:mongoPro,总传输数量:474281344,已写入条数:474281344,用时:6437s,平均写入速度:73672 per/s
 INFO  -- Program:mongoPro,本轮(10s)平均写入速度:51052 per/s
 INFO  -- Program:mongoPro,状态:2
 INFO  -- Program:mongoPro,预估同步情况:100.00%,用时6437s
 
  ============================================================================
  Program:mongoPro,全量同步完成,用时:6448s,写入数据条数:474281344
  ============================================================================
 
```

#### 6.结论

在全量同步时，4线程读取源端数据，12线程进行写入数据。

总数据量474281344条，占用磁盘35.885GB。

用时6447秒传输完毕，平均每秒写入73672条数据，平均每秒写入5.708MB数据。

# 实时

#### 1.启动D2T

参考[QuickStart](../Install/快速启动.md)

该测试环境使用如下参数

```
# D2T.properties 配置文件
#任务名。不写则默认生成
taskName=mongoTask
#程序名名。不写则默认生成
proName=mongoPro
#source端mongodb的url。必写
sourceDsUrl=mongodb://root:123456@192.168.3.190:27001/admin
#target端mongodb的url。必写
targetDsUrl=mongodb://root:123456@192.168.3.100:47018/admin
#同步模式,默认为all
# 全量:all  全量同步表,不同步同步期间对源表进行的操作
# 全量和实时:allAndRealTime  全量同步后,开始进行实时同步,实时同步的开始时间为全量同步的开始时间
# 全量和增量:allAndIncrement 全量同步后,仅同步同步期间对源表进行的操作。增量同步的开始时间为全量同步的开始时间,增量同步的结束时间为全量同步的结束时间
# 实时:realTime 实时同步
# 注全量和增量同步是一种特殊的全量和实时同步模式
syncMode=realTime
#全量同步时,是否按照依次同步表或多表并行同步。默认为false即多表并行同步
parallelSynchronizationMultipleTables=false
#需要同步的表,使用正则表达式书写。例如同步mongodb库下的所有表：mongodb\\..+   默认同步全部表：.+
dbTableWhite=photon\\..+
# 需要同步的DDL
# 实时同步情况下可以同步drop,create,createIndexes,dropIndexes,renameCollection,convertToCapped,dropDatabase。默认值为*,即同步所有DDL操作
# 多个DDL中间使用英文逗号隔离。若多个DDL中包含*,则同步所有DDL操作
ddlFilterSet=*
#全量同步情况下:是否删除目标库已经存在的源表。默认false即不删除
autoDropExistDbTable=true
#全量同步情况下:是否同步源表的索引信息。默认true即同步。在true时,当源表数据同步60%时开始同步源表的索引
autoCreateIndex=true
#全量同步情况下读取源表的线程数。最小为2，最大为50。默认值为2
sourceThreadNum=4
#全量同步情况下执行写入目标库的线程数。最小为4，最大为50 。默认值为6
#建议targetThreadNum是sourceThreadNum的3倍
targetThreadNum=12
##下面三个参数cacheBucketSize,cacheBucketNum,dataBatchSize共同决定全量情况下,内存中缓存的数据条数,注意内存溢出的情况。
##均采用默认值则内存缓存20*20*128条数据,若每条数据100kb,则最大占用内存4.88G
#每个缓存桶缓存批次数量。默认为20
cacheBucketSize=10
#缓存区个数。默认为20
cacheBucketNum=60
#每批次数据的大小。默认为128
dataBatchSize=128
#在实时同步时,设置读取oplog的开始时间。默认值为程序启动时刻的10位时间戳，否则则书写10位时间戳
startOplogTime=
#在实时同步时,设置读取oplog的结束时间。默认值为0即没有结束时间，否则则书写10位时间戳
endOplogTime=
#在实时同步时,设置读取oplog的延迟时间。默认值为0即没有延迟时间
delayTime=
#在实时同步中每个数据源解析数据的线程。最小为4，最大为50。默认值为8
realTimeThreadNum=15
#allAndRealTime模式下,全量和实时轮转进行。每次轮转时间rotationTime单位秒s，默认为0即不进行轮转
#先全量，再实时 性能佳但是可能出现oplog被覆盖。轮转 性能不佳,oplog一般情况下不被覆盖
#rotationTime=0
```

#### 2.源端插入数据

```
源端启动脚本进行CRUD操作
脚本对10张表进行CRUD操作
单条插入数据模型
{
	"_id" : ObjectId("61bad4f68a27d20b123ed7e8"),
	"BsonTimestamp1" : Timestamp(1639634166, 78),
	"String" : "str",
	"Doc" : {
		"1" : 1
	},
	"javaInt" : 71916,
	"bytes" : BinData(0,"AQ=="),
	"Array" : [ ],
	"Binary data" : BinData(0,"AQID"),
	"ObjectId" : ObjectId("61bad4f68a27d20b123ed7e6"),
	"Boolean" : false,
	"Date" : ISODate("2021-12-16T05:56:06.688Z"),
	"Null" : null,
	"Regular Expression" : /lhp.*/,
	"DBPointer" : DBPointer("1", ObjectId("61bad4f68a27d20b123ed7e7")),
	"Undefined" : undefined,
	"JavaScript" : {
		"code" : "var i=0"
	},
	"Symbol" : "var i=0",
	"BsonStr" : "var i=0",
	"BsonJavaScriptWithScope" : {
		"code" : "var i=0",
		"scope" : {

		}
	},
	"32integer" : 12,
	"Timestamp" : ISODate("2021-12-16T05:56:06.688Z"),
	"64int" : NumberLong(123),
	"Min key" : { "$minKey" : 1 },
	"Max key" : { "$maxKey" : 1 },
	"BsonTimestamp" : Timestamp(1639634166, 457)
}
源端CURD并发量共10w/s

```

#### 3.查看D2T运行情况

```
cd D2T
tail -f logs/log.log

 INFO  -- Program:mongoPro,实时同步运行:391s,读取第23次百万数据,平均58823 per/s
 INFO  -- Program:mongoPro,读取oplog延迟99s
 INFO  -- Program:mongoPro,当前实时同步缓存数:73728
 INFO  -- Program:mongoPro,当前桶批数据缓存数:0
 INFO  -- Program:mongoPro,当前表数据缓存数:0
 INFO  -- Program:mongoPro,状态:5
 INFO  -- Program:mongoPro,实时线程状态:{oplogNS=1, oplogWrite=12, oplogRead=1, oplogNsBucket=4}
 INFO  -- Program:mongoPro,写入/执行条数:23395835,写入情况:{insert=23381962, update=4339, cmd=0, delete=9534}
 INFO  -- Program:mongoPro,本轮(10s)写入/执行情况:59513 per/s
 
 
 INFO  -- Program:mongoPro,实时同步运行:821s,读取第48次百万数据,平均58465 per/s
 INFO  -- Program:mongoPro,读取oplog延迟216s
 INFO  -- Program:mongoPro,当前实时同步缓存数:28083
 INFO  -- Program:mongoPro,当前桶批数据缓存数:0
 INFO  -- Program:mongoPro,当前表数据缓存数:3370
 INFO  -- Program:mongoPro,状态:5
 INFO  -- Program:mongoPro,实时线程状态:{oplogNS=1, oplogWrite=12, oplogRead=1, oplogNsBucket=4}
 INFO  -- Program:mongoPro,写入/执行条数:48218471,写入情况:{insert=48193690, update=7526, cmd=0, delete=17255}
 INFO  -- Program:mongoPro,本轮(10s)写入/执行情况:63897 per/s
 
```

#### 4.结论

在实时同步时，源端CURD并发量共10w/s

目标端平均每秒执行58000条数据

源端CURD数据量过大时会造成D2T无法及时同步源表Oplog。及时观察'读取oplog延迟xxxs'数据，避免读取oplog时，错过滑动窗口时间。



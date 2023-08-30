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

#### 4.启动DDT

参考[QuickStart](../Install/快速启动.md)

该测试环境使用如下参数

```

# DDT.properties 配置文件
#任务名。不写则默认生成workNameDefault。
workName=mongoTask
#source端mongodb的url,必写。可以rul为单节点,复制集,分片
sourceDsUrl=mongodb://192.168.12.200:24578
#sourceDsUrl=mongodb://192.168.12.100:3999
#target端mongodb的url,必写。可以rul为单节点,复制集,分片
targetDsUrl=mongodb://192.168.12.100:24578
#同步模式  默认为all
# all  全量,全量同步表,不同步同步期间对源表进行的操作
syncMode=all
# 全量任务时，选择使用sync还是reactive
# sync:传输稳定
# reactive:速度更快
fullType=reactive
#需要同步的表，使用正则表达式书写。例如同步mongodb库下的所有表：mongodb\\..+   默认同步全部表：.+
dbTableWhite=.+
#全量同步情况下读取源端任务线程数，最小为2，最大为100。默认值为系统计算值
sourceThreadNum=10
#全量同步情况下写入到目标端任务线程数，最小为4，最大为100 。默认值为系统计算值  建议targetThreadNum是sourceThreadNum的三倍
targetThreadNum=20
#全量同步情况下建立索引并发线程数，最小为1，最大为100 。默认值为系统计算值
createIndexThreadNum=15
##下面三个参数bucketSize,bucketNum,batchSize共同决定全量情况下,内存中缓存的数据条数,注意内存溢出的情况。
##均采用默认值则内存缓存20*20*128条数据,若每条数据100kb,则最大占用内存4.88G
#每批次数据的大小 默认为128
batchSize=128
#缓存桶个数  默认为20
bucketNum=20
#每个缓存桶缓存批次数量  默认为20
bucketSize=20
#同步中 每个DDL操作最大耗时 单位s
ddlWait=1200
# 全量同步时
# 数据传输前，预处理：同步集群中DDL信息
# 0:全量同步时 是否删除目标端已经存在的表
# 1:打印输出集群全部用户信息
# 2:同步库表表结构
# 3:同步库表索引信息
# 4:全部库开启库分片
# 5:同步库表shard key
# 6:同步config.setting表
# 7:库表预切分chunk
# 可以组合使用 例如 1,2,3,4,5,6  1,2,3,7 默认值为空
# 组合用逗号隔开
clusterInfoSet=0,1,2,3,4,5,6,7
# 开启monitor监控时,配置的本机ip地址
bind_ip=192.168.12.190

```


#### 5.结论

在全量同步时，4线程读取源端数据，12线程进行写入数据。

总数据量474281344条，占用磁盘35.885GB。

用时6447秒传输完毕，平均每秒写入73672条数据，平均每秒写入5.708MB数据。

# 实时

#### 1.启动DDT

参考[QuickStart](../Install/快速启动.md)

该测试环境使用如下参数

```
# DDT.properties 配置文件
#任务名。不写则默认生成workNameDefault。
workName=mongoTask
#source端mongodb的url,必写。可以rul为单节点,复制集,分片
sourceDsUrl=mongodb://192.168.12.200:24578
#sourceDsUrl=mongodb://192.168.12.100:3999
#target端mongodb的url,必写。可以rul为单节点,复制集,分片
targetDsUrl=mongodb://192.168.12.100:24578
#同步模式  默认为all
# realTime 实时。开始时间和结束时间可以配置startOplogTime,endOplogTime
syncMode=realTime
# 实时或者增量任务时，选择使用oplog还是changestream
# 选择oplog,特点:源端为复制集,可以同步DDL,速度更快
# 选择changestream,支持:源端为复制集或mongos,不支持DDL,速度一般
realTimeType=changestream
#需要同步的表，使用正则表达式书写。例如同步mongodb库下的所有表：mongodb\\..+   默认同步全部表：.+
dbTableWhite=.+
# 实时同步情况下可以同步drop,create,createIndexes,dropIndexes,renameCollection,convertToCapped,dropDatabase,modify,shardCollection
# 默认值为 * ,代表同步所有DDL操作
# 需要同步的DDL，多个ddl中间使用英文逗号隔离
ddlFilterSet=*
##下面三个参数bucketSize,bucketNum,batchSize共同决定全量情况下,内存中缓存的数据条数,注意内存溢出的情况。
##均采用默认值则内存缓存20*20*128条数据,若每条数据100kb,则最大占用内存4.88G
#每批次数据的大小 默认为128
batchSize=128
#缓存桶个数  默认为20
bucketNum=20
#每个缓存桶缓存批次数量  默认为20
bucketSize=20
#在实时同步时,设置读取oplog的开始时间,默认值为程序启动时刻的10位时间戳
startOplogTime=1692843646
#在实时同步时,设置读取oplog的结束时间,默认值为0即没有结束时间，否则则书写10位时间戳
endOplogTime=1692847246
#在实时同步时,设置读取oplog的延迟时间,默认值为0即没有延迟时间
delayTime=0
#在实时同步中解析桶的线程数的线程数,最小为8，最大为100。默认值为系统计算值
nsBucketThreadNum=15
#在实时同步中写数据的线程数的线程数,最小为8，最大为100。默认值为系统计算值
writeThreadNum=15
#同步中 每个DDL操作最大耗时 单位s
ddlWait=1200

# 开启monitor监控时,配置的本机ip地址
bind_ip=192.168.12.190

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



#### 3.结论

在实时同步时，源端CURD并发量共10w/s

目标端平均每秒执行58000条数据

源端CURD数据量过大时会造成DDT无法及时同步源表Oplog。及时观察'读取oplog延迟xxxs'数据，避免读取oplog时，错过滑动窗口时间。



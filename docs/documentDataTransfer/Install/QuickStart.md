## QuickStart

## 启动步骤

#### 1.下载D2T

  访问 https://github.com/whaleal/D2T/releases

  下载最近版本的D2T.tar.gz

#### 2.解压缩

```
mkdir D2T
tar -zxvf mngodbT.tar.gz  -C D2T
```

#### 3.配置文件修改
[配置介绍](./Configuring.md)

```
cd D2T/config
vi D2T.properties
```


#### 4.准备启动

```
cd bin
./start.sh
```

#### 5.查看日志

```
cd logs/
tail -f logs.log
tail -f error.log
```

#### 6.查看目标端的数据量，对比数据一致性。

1 使用mongodb自带校验工具。（会锁库）

```
 use xxx
 db.runCommand({dbHash:1})
 ```

2 手动校验数据
```
java -jar checkData.jar /配置文件路径/D2T.properties
```

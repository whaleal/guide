## QuickStart

## 启动步骤

#### 1.下载DDT

  访问 https://github.com/whaleal/DocumentDataTransfer/releases

  下载最近版本的DDT.tar.gz

#### 2.解压缩

```
mkdir DDT
tar -zxvf DDT.tar.gz  -C DDT
```

#### 3.配置文件修改
[配置介绍](Configuring.md)

```
cd DDT/config
vi DDT.properties
```


#### 4.准备启动

```
cd bin
./start-all.sh
```

#### 5.查看运行情况

```
访问web监控页面
http://bind_ip:58000/DDT_WEB/#/home
```


#### 6.查看目标端的数据量，对比数据一致性。

1 使用mongodb自带校验工具。（会锁库）

```
 use xxx
 db.runCommand({dbHash:1})
 ```

2 手动校验数据
```
java -jar checkData.jar /配置文件路径/DDT.properties
```
